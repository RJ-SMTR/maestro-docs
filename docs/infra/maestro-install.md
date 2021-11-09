# Instalação do Maestro para desenvolvimento local

## Requisitos de software

- Docker
- Python >= 3.8 (outras versões não são testadas)

## Pré-configuração

- Clonar o repositório oficial do Maestro e acessá-lo

```
git clone https://github.com/RJ-SMTR/maestro
cd maestro/
```

- No seu ambiente virtual de preferência (ou sem ele), instale o aplicativo de linha de comando do maestro

```
# cria ambiente virtual chamado venv (ou .env, conforme .gitignore)
python -m venv venv
# instala dependencias
pip install -r .
```

- Prepare um arquivo de variáveis de ambiente chamado `.env_local`. Ele deve seguir o seguinte modelo (preencher somente onde é requisitado, instruções abaixo):

```
MODE=dev
DAGSTER_POSTGRES_USER=postgres
DAGSTER_POSTGRES_PASSWORD=123456
DAGSTER_POSTGRES_HOST=localhost
DAGSTER_POSTGRES_DB=postgres
REDIS_HOST=localhost
BQ_PROJECT_NAME=rj-smtr-dev
SENSOR_BUCKET=rj-smtr-dev
BASEDOSDADOS_CONFIG=<preencher>
BASEDOSDADOS_CREDENTIALS_PROD=<preencher>
BASEDOSDADOS_CREDENTIALS_STAGING=<preencher>
DAGSTER_HOME=<preencher>
```

- Preencha `DAGSTER_HOME` com o caminho do repositório do maestro + `.dagster_workspace`. Exemplo: `/home/user/git_repos/maestro/.dagster_workspace`

- Preencha `BASEDOSDADOS_CONFIG` com o resultado de `cat $HOME/.basedosdados/config.toml | base64`, considerando que você possui as credenciais de **DEV**

- Preencha `BASEDOSDADOS_CREDENTIALS_PROD` e `BASEDOSDADOS_CREDENTIALS_STAGING` com o resultado de `cat .basedosdados/credentials/prod.json | base64`, considerando que você possui as credenciais de **DEV**

## Configuração

- Para configurar o ambiente todo basta, no seu ambiente virtual de preferência (ou sem ele), executar

```
maestro setup
```

## Ligando os serviços

- Para executar o ambiente de desenvolvimento basta, no seu ambiente virtual de preferência (ou sem ele), executar

```
maestro up
```

- Com isso, o Dagit ficará disponível em http://localhost:3000/ e os logs do daemon, dagit e gRPC serão todos redirecionados ao mesmo terminal.
