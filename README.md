# Portaria Blindada

Plataforma própria de inteligência operacional e verificação de informações para apoio à segurança e ao controle de acesso do Residencial Valville.

> **Status:** especificação do MVP, 19/10/2026. Ainda não há integração ativa com provedores judiciais ou sistemas locais. **Não utilizar dados reais em protótipos.**

## Visão
Construir ferramenta independente do Condomínio Blindado, com consultas **diretamente na plataforma** desde a primeira versão, resultados verificáveis, fontes documentadas, histórico e análise humana. Integração futura com **iControl e Secure**, instalados on-premises no Valville, condicionada à resposta técnica da **Avato**. Escopo atual: uso interno do Valville; futura comercialização **não** faz parte do MVP.

## Princípios
- Prioridade à **velocidade na entrada**, sem comprometer acurácia ou inventar resultado quando uma fonte estiver indisponível.
- Nenhuma pessoa é classificada como perigosa apenas por registros judiciais ou algoritmo; processo não equivale a condenação, e homônimos não podem gerar conclusão automática.
- Nenhum bloqueio de acesso automatizado por apontamento judicial. Procedimentos e decisões sensíveis cabem à equipe humana autorizada.
- Finalidade, minimização, acesso restrito, auditoria, retenção limitada e avaliação jurídica/LGPD antes de operar com dados reais.
- Não contornar CAPTCHA, restrições técnicas, termos de uso ou limites de automação de bases públicas.
- Consulta a provedores somente com acesso e finalidade autorizados.

## MVP — prioridades
1. Autenticação e perfis: operador da portaria, segurança, administrativo, auditor (acesso mínimo necessário).
2. **Consulta manual** por CPF, nome e categoria (prestador, visitante, outros), com validação e registro da finalidade. Até autorização/homologação, operar **apenas com dados fictícios e fontes simuladas**.
3. Motor assíncrono de consulta com conectores substituíveis, execução paralela quando permitida, timeout e atualização automática de status.
4. Estados explícitos: não iniciada, processando, parcialmente concluída, concluída, inconclusiva, indisponível/erro. **Ausência de achado** não equivale a atestado de inexistência de antecedentes.
5. Resultado auditável por fonte: origem, data da coleta, cobertura, correspondência de identidade, limitações, validade e evidências, com mascaramento de dados em telas não autorizadas.
6. Reconsulta de resultados previamente verificados apenas dentro de prazos válidos e quando compatível com a finalidade.
7. Fila de revisão humana, registros de providências e trilha de auditoria.
8. Painel gerencial, indicadores diários/acumulados, fila de pendências e Modo TV **sem exposição de dados pessoais sensíveis**.
9. Alertas a responsáveis autorizados, com conteúdo mínimo, sem detalhamento sensível em notificações inseguras.
10. Integração futura com iControl/Secure mediante interface homologada pela Avato; preservar operação independente dos controladores atuais.

## Metas iniciais de desempenho (a validar)
- Histórico verificado ainda válido: interface em até **1 segundo** (meta).
- Resposta preliminar de pesquisa inédita: até **5 segundos** (meta, **não** garantia).
- Finalização de pesquisa inédita: até **30 segundos**, dependendo da fonte (meta).
- Respostas parciais nunca apresentadas como conclusivas; métricas p50/p95/p99, disponibilidade, timeout e taxa de inconclusivos.

## Stack proposta (não implementada)
Next.js + TypeScript; PostgreSQL/Neon; hospedagem Vercel para a aplicação; serviço/conector local seguro para integrações on-premises (sujeito a arquitetura e documentação Avato). Credenciais somente em armazenamento de segredos; nunca versioná-las.

## Pendências externas
- Resposta da **Avato**: API/SDK, eventos, campos, modo leitura, regras de escrita, autenticação e conectividade segura com iControl/Secure.
- Identificar e homologar fornecedores de dados: termos, abrangência, atualização, custo, direitos de tratamento e níveis de serviço.
- Parecer jurídico/LGPD e avaliação de impacto antes de consultas de pessoas reais.
- Estabelecer o POP da portaria para resultados inconclusivos, homônimos e eventuais alertas críticos.

## Documentação
- [Requisitos e critérios de aceite](docs/MVP.md)
- [Arquitetura e decisões](docs/ARQUITETURA.md)
- [Roadmap e dependências](docs/ROADMAP.md)

## Referência econômica
Proposta do fornecedor estudada em 19/10/2026: faixa estimada de 2.200–2.500 consultas/mês e preço de referência de R$ 3,63 por consulta; custo projetado de R$ 7.986–9.075/mês. Estes números são **referências para análise**, não comprovação do custo da Portaria Blindada.
