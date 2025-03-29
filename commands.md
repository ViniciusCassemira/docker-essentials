# Comandos básicos do Docker 🖥️📜

## 🔍 Verificar versão e informações
#### Verifica a versão instalada
```sh
docker --version
```
#### Exibe informações detalhadas sobre a instalação
```
docker info
```

## 🛠 Trabalhando com Imagens

#### Lista as imagens que você tem em sua máquina 
```sh
docker images
```

#### Remove uma imagem local
```sh
docker rmi <imagem>
```

#### Realiza uma marcação (tag) em uma imagem com um nome específico
```sh
docker tag <imagem> usuario/nome:versao
```

## Docker Containers

#### Inicia um container em segundo plano
```sh
docker run -d -p 8080:80 <container>
```

<details>
  <summary>Sobre os parâmetros <code>-d</code> e <code>-p</code></summary>

  - **`-d` (detached mode)**: Faz com que o contêiner seja executado em segundo plano, ou seja, ele não trava o terminal e continua rodando mesmo após o encerramento da sessão.
  
  - **`-p 8080:80` (port mapping)**: Mapeia a porta do host para a porta do contêiner.
    - O primeiro número (`8080`) representa a porta do host (seu computador).
    - O segundo número (`80`) representa a porta do contêiner onde a aplicação está rodando.
    - Assim, ao acessar `http://localhost:8080`, você estará se comunicando com o serviço dentro do contêiner na porta `80`.

</details>

#### Lista containers em execução na sua máquina naquele momento
```sh
docker ps       
```

#### Lista todos os containers existentes em sua máquina (executando ou parados)
```sh
docker ps -a    
```

#### Para um container que esteja em execução
```sh
docker stop <container>   
```

#### Inicia um container que esteja parado
```sh
docker start <container>   
```
#### Remove um container existente
```sh
docker rm <container>
```

#### Restarta o container
```sh
docker restart <container>
```

#### Pausa o container
```sh
docker pause <container>
```

#### Retoma(despausa) o container
```sh
docker unpause <container>
```

#### Executar comandos dentro do nosso container
```sh
    docker exec -it <nome-container> /bin/bash
```

## 📦 Trabalhando com Volumes

#### Criando um volume nomeado  
```sh
docker volume create <nome-volume>
```

#### Criar um container e vincular a um volume existente 
```sh
docker run --name db -v <nome-do-volume>:/var/lib/mysql mysql
```
Acabamos de criar um container chamado **db** a partir da imagem do **MySQL** e vinculamos o repositório **/var/lib/mysql** do nosso container ao volume que criamos. Dessa forma, todos os dados que forem adicionados nesse caminho do container ficarão armazenados em nosso volume.

#### Criando um volume anônimo  
```sh
docker run -v /var/lib/mysql mysql
```
Nesse caso, um volume anônimo é montado no diretório **/var/lib/mysql** dentro do container **MySQL**.

#### Visualizar todos os volumes existentes  
```sh
docker volume ls
```

#### Remover um volume específico  
```sh
docker volume rm <nome-do-volume>
```
Para apagar um volume, certifique-se de que nenhum container esteja o utilizando.

#### Apagar volumes não utilizados  
```sh
docker volume prune
```
Isso excluirá todos os volumes não utilizados por containers ativos.

#### Inspecionar um volume específico  
```sh
docker volume inspect db_data
```

## 🔗 Trabalhando com Redes

#### Criando uma network do tipo bridge
```sh
docker network create -d bridge my-net
```

#### Lista redes disponíveis
```sh
docker network ls                     
```

#### Inspeciona detalhes de uma rede
```sh
docker network inspect minha-rede 
```

#### Remove uma rede
```sh
docker network rm minha-rede          
```

#### Rodando um container e adicionando ele dentro da nossa network já criada
```sh
docker run --network=minha-rede --name=container busybox
```

#### Conectar um container à uma network
```sh
docker network connect <network-name> <container-name>
```

#### Desconectar um container da network 
```sh
docker network disconnect <network-name> <container-name>
```

## DockerHub

#### Realiza o login na sua conta do DockerHub
```sh
docker login
```

#### Baixa uma imagem que esteja no Dockerhub
```sh
docker pull <imagem>
```
<details>
  <summary>Observação</summary>

  Para baixarmos uma versão específica da imagem passamos uma :tag no comando
  ```sh
  docker pull imagem:1.0 #Para baixar a versão 1.0 da imagem
  docker pull imagem:latest #Para baixar a versão mais recente
  ```
  Caso não passemos nenhuma tag ao baixar uma imagem, será baixada a sua versão mais recente

</details>

#### Adicionar uma TAG em sua imagem local
```sh
docker tag <image-name> <docker-username>/<image-name>:<tag>
```

#### Subir uma imagem local para o Dockerhub
```sh
docker push <docker-username>/<image-name>:<tag>
```

## Docker compose
em breve