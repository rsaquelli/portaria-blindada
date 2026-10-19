# Roadmap de execução

Referência: 19/10/2026. Todos os itens abaixo estão **pendentes**; este commit documenta o projeto e não constitui aplicação implantada.

## Etapa 0 — fundação
- [ ] Configurar Next.js/TypeScript e qualidade de código.
- [ ] Definir ambiente dev/staging, Neon, migrações e gestão de segredos.
- [ ] Implementar autenticação, papéis, autorização, auditoria e dados fictícios.

## Etapa 1 — consulta manual (prioridade máxima)
- [ ] Formulário CPF/nome/tipo/finalidade e validação.
- [ ] API de abertura de consulta e status com idempotência.
- [ ] Workers e adaptador mock, atualização visível de progresso.
- [ ] Resultado com fonte, data, cobertura, validade e estado correto.
- [ ] Histórico de consultas, pesquisa restrita e reuso somente se válido.
- [ ] Fila de revisão humana, providências e POP de contingência.

## Etapa 2 — operação
- [ ] Dashboard, indicadores diários e acumulados.
- [ ] Modo TV sem dados pessoais sensíveis.
- [ ] Alertas restritos, auditoria e métricas de desempenho.
- [ ] Testes de carga e de falhas; alvos p95, documentação operacional.

## Etapa 3 — fontes de dados reais (gate obrigatório)
- [ ] Estudo comparativo de fontes e provedores.
- [ ] Aprovação jurídica/LGPD, documentação da finalidade e avaliação de impacto.
- [ ] Contrato/licença e credenciais de sandbox.
- [ ] Homologação de precisão, homônimos, cobertura, atualização, custo e SLA.
- [ ] Ativação controlada para dados reais somente após aprovação.

## Etapa 4 — integração Avato
- [ ] Receber documentação iControl e Secure, on-premises.
- [ ] Confirmar campos, eventos, API/webhook/SDK e limites do fabricante.
- [ ] Conector local seguro com eventos idempotentes.
- [ ] Sincronização de cadastros e gatilho de consulta quando autorizado.
- [ ] Garantir que a consulta manual permaneça disponível.
- [ ] Contingência: sistemas de acesso locais independentes.

## Critérios de avanço
Nada em produção com dados reais sem fonte homologada, aprovação jurídica, controles de acesso, revisão humana, POP de contingência e validação de desempenho. Priorizar qualidade da informação e fluidez da portaria.
