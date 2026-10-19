# Arquitetura e decisões técnicas — Portaria Blindada

## Contexto
Produto **independente** do Condomínio Blindado. Primeiro cliente e única implantação prevista: Valville. Portaria precisa consultar na hora da entrada; integração com iControl e Secure (ambos on-premises) ainda não disponível, aguardando Avato.

## Componentes
1. **Web Next.js/TypeScript**: painel, consulta manual, resultado e fila; autenticação e autorização no servidor.
2. **API interna**: valida entrada, autoriza consulta, gera protocolo e retorna status; não expõe credenciais nem dados de provedores ao navegador.
3. **Fila de jobs**: despacho idempotente, concorrência controlada, retries limitados, limite de tempo e detecção de provedores indisponíveis. Escolher infraestrutura compatível com execução durável, não depender de execução longa em requisição web.
4. **Adaptadores**: interface tipada; conectores simulados para desenvolvimento; reais somente após contrato, documentação, testes e aprovação jurídica.
5. **Persistência PostgreSQL/Neon**: pessoas mínimas, finalidades, consultas, achados separados por fonte, estados, evidências autorizadas, auditoria, revisão e política de expurgo.
6. **Conector local futuro**: serviço na rede Valville para iControl/Secure por interfaces oficiais; comunicação de saída autenticada e cifrada, sem exposição direta de banco local. Operação do controle de acesso deve sobreviver à indisponibilidade da Portaria Blindada.

## Fluxo consulta manual
Operador autenticado → valida CPF e finalidade → busca consulta reutilizável ainda válida → se não houver, gera job → estado 'processando' → executa adaptadores habilitados → normaliza campos, identidade/cobertura e carimbo temporal → estado parcial/concluído/inconclusivo → eventual revisão humana → registro auditável.

## Modelo lógico inicial
- User, Role, Session
- Person (CPF cifrado; busca com índice pseudonimizado; mascaramento por perfil)
- AccessContext (prestador/visitante/outro, solicitação, finalidade)
- VerificationRequest (identificador, autor, data, status, tempos)
- SourceCheck (provedor, versão, cobertura, status, consultadoEm, venceEm, evidência)
- Finding (categoria documental, correspondência de identidade, dados mínimos autorizados, necessidades de revisão)
- ReviewDecision (revisor, justificativa, momento e encaminhamento)
- AuditEvent (acesso, consulta, leitura sensível, alteração, expurgo)
- IntegrationEvent (futuro: evento externo idempotente, origem e status)

## Regras de segurança
- Isolamento por perfil, permissões explícitas no backend, MFA para perfis sensíveis, logging sem CPF bruto ou tokens.
- Não publicar chaves, credenciais, registros reais ou capturas sensíveis neste repositório.
- Cache por fonte/finalidade/validade definida, com revogação e trilha de origem. Nunca assumir que ausência de achado significa ausência de antecedentes.
- IA pode resumir evidências verificadas, mas não atribuir score de 'periculosidade' nem decidir entrada.
- Avaliar base legal, transparência, direitos do titular, RIPD, retenção e contratos de operador/controlador antes de operar.
- Interface de evento externo somente após homologação do fabricante, sem engenharia reversa invasiva.

## SLA e observabilidade
Metas propostas: cache válido em 1 s; status preliminar 5 s; tentativa de conclusão em 30 s para novas consultas. Tolerar provedores lentos, informar cobertura incompleta e permitir contingência humana. Registrar latência por adaptador, p95, falhas, qualidade da identidade e auditoria de acesso.

## Decisões em aberto
- Avato: API, SDK, webhook, leitura/escrita, topologia, autenticação.
- Quais fontes são legal e tecnicamente elegíveis, contratos, custo real e SLA.
- Hospedagem de workers, fila, retenção e armazenamento seguro de documentos.
- POP de acesso, critérios de revisão, responsáveis e escalonamentos.
