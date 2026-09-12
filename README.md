# Giro

**Agenda, caixa e clientes para o pequeno negócio.**

O Giro é uma plataforma SaaS/PWA em português do Brasil para pequenos negócios e prestadores de serviços. Centraliza agenda, clientes, caixa, ordens, equipe, backups, cobrança Pix e planos comerciais, com painel administrativo exclusivo do CEO.

## Status

- Aplicação web/PWA: ativa
- Autenticação e nuvem: ativas
- Vários negócios por conta: ativo
- Cadastro por segmento: ativo
- Painel CEO: ativo
- Integração Asaas: implementada
- Backups em nuvem: ativos

## Desenvolvimento

Desenvolvedor e CEO administrador: **Carlos Alisson Silva Falcão Lins**.

## Segurança

Credenciais e segredos de produção não são versionados neste repositório. `ASAAS_API_KEY` e demais segredos devem ser configurados no ambiente seguro de deploy.

## Executar localmente

```bash
npm install
npm run dev
```

Para gerar a build:

```bash
npm run build
```

## Estrutura

- `src/` — frontend React/TypeScript
- `backend/` — API, nuvem, billing, administração e webhook
- `public/` — PWA, ícone e service worker
- `tests/` — cenários funcionais documentados
- `appdeploy.auth-login.json` — configuração visual de autenticação

A documentação funcional e técnica detalhada também está mantida no Notion da Impulso MKT Digital.
