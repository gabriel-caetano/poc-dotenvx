# poc-dotenvx
[Documentação](https://dotenvx.com/docs)

Gerenciamento seguro de variáveis de ambiente, projetada para ser simples de usar.
Baseado em criptografia para permitir o compartilhamento dos arquivos .env de forma segura através do GitHub.

### Implementação

Add buildpack no heroku:
`heroku buildpacks:add https://github.com/dotenvx/heroku-buildpack-dotenvx`

Alterar Procfile para executar através do dotenvx
`web: dotenvx run -- node index.js`
opcional: usar flag `-f .env` para usar um env diferente

Encriptar arquivos .env
`dotenvx encrypt -f .env`
se não existir, será criado o arquivo `.env.keys` com a chave privada
essa chave deverá ser adicionada no env do heroku como `DOTENV_PRIVATE_KEY_PRODUCTION`

Os arquivos `.env` devem ser commitados normalmente,
com todas as informações criptografadas e a chave pública
O arquivo `.env.keys` deve ser ignorado no `.gitignore`

A única informação que deve ficar nas config vars do heroku é a chave privada,
todo o resto será injetado pelo dotenvx
