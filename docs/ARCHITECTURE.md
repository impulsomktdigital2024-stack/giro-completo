# Arquitetura do Giro

## Visão geral

O Giro é uma aplicação React + TypeScript distribuída como PWA e acompanhada de um backend server-side baseado no SDK do AppDeploy.

```text
PWA React/TypeScript
        |
        | autenticação + API
        v
Backend Giro
  |-- dados multi-tenant
  |-- backups
  |-- painel CEO
  |-- billing
  |-- webhook Asaas
        |
        +------> Asaas API
```

## Frontend

`src/Giro.tsx` concentra a experiência operacional: agenda, caixa, clientes, ordens, equipe, Pix do estabelecimento, backups, planos e integrações.

`src/AdminPanel.tsx` implementa a área exclusiva do CEO para métricas, contas, empresas, planos, pagamentos e auditoria.

`src/BusinessSetupForm.tsx` e `src/businessProfiles.ts` implementam o onboarding por segmento e os serviços iniciais sugeridos.

## Backend

`backend/index.ts` implementa as rotas protegidas e os índices globais necessários à administração do SaaS.

Principais grupos de endpoints:

- `/api/businesses*` — CRUD dos negócios e backups.
- `/api/integrations/*` — status e configuração das integrações.
- `/api/billing/*` — assinatura comercial do Giro.
- `/api/webhooks/asaas` — atualização automática do plano conforme cobrança.
- `/api/admin/*` — gestão exclusiva do CEO.

## Multi-tenant

Cada usuário autenticado possui tabelas lógicas próprias para negócios, backups e controle de acesso. Um índice administrativo separado agrega somente os dados necessários ao painel do CEO.

## Persistência local e nuvem

Sem autenticação, o Giro usa `localStorage` (`giro-v2`) e mantém migração do legado `giro-v1`. Ao autenticar, a operação passa a usar a camada de dados em nuvem; quando uma conta não tem negócio e existe uma operação local, ela pode servir como semente inicial.

## Pagamentos

A assinatura do SaaS usa Asaas com cobrança mensal por Pix. A chave de API nunca fica no frontend. O webhook confirma recebimento e atualiza o plano no backend.

O Pix cadastrado pelo estabelecimento é diferente: ele gera um payload EMV Copia e Cola para o cliente final, sem consulta bancária automática.

## PWA

`public/manifest.webmanifest`, `public/sw.js` e `public/icon.svg` permitem instalação na tela inicial e cache do shell principal.
