# Operação e Deploy

## Ambiente principal

O código desta versão foi extraído da versão aplicada do Giro no AppDeploy. O SDK `@appdeploy/client` no frontend e `@appdeploy/sdk` no backend fazem parte dessa arquitetura de execução.

## Segredos necessários

- `ASAAS_API_KEY` — chave do ambiente Asaas. O backend detecta produção quando a chave começa com o prefixo de produção; caso contrário usa sandbox.

Não coloque o valor da chave neste repositório.

## Webhook Asaas

Após autenticar no Giro, abra **Conexões**. Se a API Asaas estiver configurada, o sistema pode registrar/revalidar automaticamente o webhook em:

`https://<dominio-do-giro>/api/webhooks/asaas`

Eventos acompanhados:

- `PAYMENT_CREATED`
- `PAYMENT_CONFIRMED`
- `PAYMENT_RECEIVED`
- `PAYMENT_OVERDUE`
- `PAYMENT_REFUNDED`

## Backup

O Giro mantém pontos de restauração manuais e cria backup automático antes de alterações quando o último backup automático tem mais de 24 horas. Também existe exportação JSON no frontend.

## CEO

A administração server-side é liberada somente para os e-mails definidos em `ADMIN_EMAILS` no backend. O CEO consegue visualizar contas e negócios, bloquear/liberar clientes, alterar plano operacional, consultar dados do Asaas e revisar auditoria.

## Testes

Os cenários funcionais estão em `tests/tests.txt`. A versão implantada que originou este repositório passou pelo QA de build/runtime do AppDeploy sem erros de frontend, rede ou backend. O arquivo de cenários E2E está versionado como especificação; não deve ser confundido com prova de execução automatizada de todos os cenários.

## Antes de publicar alterações

1. Não adicionar segredos ao Git.
2. Conferir TypeScript e build no ambiente AppDeploy.
3. Validar login e isolamento entre usuários.
4. Testar criação/edição de negócio e segmento.
5. Validar conclusão de atendimento sem duplicar caixa.
6. Validar conflito de horários por profissional.
7. Validar backups.
8. Se houver mudança financeira, testar primeiro com Asaas Sandbox.
9. Confirmar que usuário comum não acessa `/api/admin/*`.
