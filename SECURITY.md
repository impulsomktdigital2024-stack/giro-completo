# Segurança do Giro

## Segredos

Nunca versionar chaves de API, tokens de webhook, credenciais de banco, cookies de sessão ou arquivos `.env` reais.

O backend referencia o segredo `ASAAS_API_KEY`, mas o valor deve existir somente no cofre seguro do ambiente de deploy.

## Administração

As rotas `/api/admin/*` exigem autenticação e validação server-side da allowlist administrativa. A interface do Painel CEO não é a barreira de segurança; o backend é responsável pela autorização.

## Webhook Asaas

O Giro cria um token aleatório para o webhook, armazena apenas o hash SHA-256 e valida o cabeçalho `asaas-access-token`. Eventos são registrados por ID para evitar processamento duplicado.

## Isolamento de clientes

Dados operacionais são particionados por `userId`, e cada negócio possui um identificador próprio. O índice global usado pelo CEO contém metadados de gestão, não credenciais.

## Reporte

Falhas de segurança devem ser tratadas de forma privada antes de qualquer divulgação pública.
