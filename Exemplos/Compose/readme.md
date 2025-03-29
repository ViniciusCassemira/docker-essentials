# Rodando o Docker Compose

Para rodar o **Docker Compose** corretamente e capturar as variáveis do arquivo `.env`, execute o seguinte comando dentro da pasta do Compose:

```sh
docker compose --env-file .env up -d
```

Espere o compose subir todos os seus serviços(containers) e pronto! Sua aplicação subiu corretamente, fazendo a configuração do seu container wordpress e do mysql. Para testar, acesse em seu navegador **localhost:8080**