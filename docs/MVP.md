# MVP — requisitos e critérios de aceite

**Versão:** 0.1 — 19/10/2026. Escopo: uso interno Valville. Requisitos especificados, ainda não implementados.

## P0 — operação sem integrações
- LOGIN-01: perfis operador, segurança, administração e auditoria com autorização server-side; sessão segura e logs de acesso.
- MAN-01: nova consulta diretamente no aplicativo. Campos CPF (validar dígitos), nome, tipo de acesso e finalidade; buscar histórico por CPF de modo restrito.
- MAN-02: feedback instantâneo ao clicar, identificador de protocolo, status e andamento sem duplo envio.
- MOTOR-01: adaptadores de fontes (mock + conectores homologados posteriormente), cada resposta com fonte, hora, cobertura, evidência e estado.
- MOTOR-02: processamento assíncrono, idempotência, timeout, filas e consultas em paralelo apenas se autorizadas.
- RES-01: separar 'sem apontamentos nas fontes consultadas', 'correspondência a verificar', 'inconclusivo', 'fonte indisponível', 'em processamento'. Nunca transformar erro ou falta de cobertura em negativo.
- RES-02: validação de homônimos e divergências de identidade; processo não comprova condenação; conferência humana obrigatória para apontamentos.
- HIST-01: trilha imutável de consulta (quem, quando, finalidade, quais fontes e versões, providências) e política de retenção configurável.
- REV-01: fila de revisão: responsável, prioridade operacional, decisão registrada e justificativa; sem decisão automática de bloquear acesso.
- DASH-01: volume por período, indicadores por status, pendências, tempos, erros, sem dados pessoais no Modo TV.
- AVISO-01: alertas a responsáveis autorizados somente com dados mínimos, sem exposição de informações criminais em telas coletivas ou WhatsApp.
- SEG-01: acesso mínimo, criptografia em trânsito e repouso, segregação entre perfis, mascaramento e proteção contra enumeração de CPF.
- PRIV-01: teste com dados fictícios até validação jurídica e autorização de provedores.

## P1 — aperfeiçoamentos
- Pré-consultas permitidas de prestadores recorrentes; validade por fonte e regra, sem reuso indefinido.
- Acompanhamento permitido de atualizações, se contratado e justificado.
- Evidências documentais de validade/autenticidade; exportação de relatórios restritos.
- Integração iControl/Secure com conector homologado e eventos em tempo real após retorno Avato.

## Cenários de aceite indispensáveis
1. Consulta nova em mock: cria protocolo e conclui com fontes e tempos demonstrativos; sinaliza explicitamente que os resultados são fictícios.
2. Repetir envio: não gera consultas duplicadas.
3. Fonte indisponível: estado 'inconclusivo/parcial', nunca 'sem registros'.
4. Homônimo: requer conferência humana; nenhuma penalização/bloqueio automático.
5. Resultado previamente válido: recupera histórico com data, fonte e limite de reutilização.
6. Sem autorização: operador não acessa resultados fora do seu perfil; Modo TV não mostra CPF ou achados criminais.
7. Falha de internet/API: exibe estado e contingência do POP, sem afetar controlador de acesso local.
8. Auditoria: registra alterações e revisão com autor, data e motivo.
9. Latência: medir p50/p95/p99 e taxa de timeout sob carga; metas são indicativas, sem garantia de terceiros.

## Fora do MVP
Comercialização SaaS, motor de cobrança, bloqueio automático de catraca, reconhecimento facial próprio, scraping de fontes que vedem automação, inferência de periculosidade e integração direta não homologada.
