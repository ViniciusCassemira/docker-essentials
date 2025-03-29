# Docker Compose 🧩🎵

Docker Compose é uma ferramenta usada para definir e gerenciar aplicativos Docker compostos através de vários containers. Ele permite configurar todos os serviços necessários para um projeto de forma declarativa, **utilizando um arquivo YAML** _(docker-compose.yml)_. Ao invés de declarar comando por comando no terminal para criar as suas configurações do ambiente como criação de network, volumes, containers, entre outros, tudo isso pode ser feito dentro do arquivo do **compose.yml**.

## Por que devo usar Docker Compose?
- **Com apenas um comando**, todos os containers da sua aplicação são iniciados com as configurações que você declarou, e toda a aplicação pode ser encerrada com outro único comando.
- Auxilia a manutenção do projeto, pois todas as configurações **se encontram em um só arquivo** (compose.yaml / docker-compose.yml).
- Facilita a conexão e configuração dos seus containers, se tornando mais fácil de visualizar e compreender o que está acontecendo.

## Estrutura Básica
```yaml
    # Declarando volumes
    volumes:
      db_system: #Volume para o MySQL

    # Declarando networks
    networks:
      app_net: #Nome da rede
        driver: bridge # Tipo da rede

    # Dentro de services nós criaremos os nossos containers
    services:
      mysql: # Nome do container
        image: mysql:8.3.0 #Imagem base
        ports: # Define o mapeamento de portas. 
          - 3306:3306 # Mapeia a porta 3306 do host para a porta 3306 do contêiner.
        environment: #Variáveis que o container vai utilizar, podendeo ser passado diretamente ou capturar a partir de um arquivo .env
          MYSQL_ROOT_PASSWORD: ${DB_ROOT_PASSWORD}
          MYSQL_DATABASE: ${DB_DATABASE}
          MYSQL_USER: ${DB_USER}
          MYSQL_PASSWORD: ${DB_PASSWORD}
        volumes: #Vinculando o volume ao repositório do container para persistência de dados
          - db_system:/var/lib/mysql
        networks: #Atrelando o container a uma rede
          - app_net
```

Nesse exemplo, **criamos uma rede** do tipo bridge, **um volume nomeado**, **um container** a partir da imagem do MySQL com algumas variáveis, além de conectá-lo em nossa network e volume.

Conheça os comandos para manipular e criar Docker Compose [clicando aqui](./commands.md).