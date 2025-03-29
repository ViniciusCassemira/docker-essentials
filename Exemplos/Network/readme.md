# Usando networks 

Nesse exemplo, vamos ver como as networks conseguem conectar container de forma simples e rápida, para que suas aplicações consigam se comunicar com os diversos containers existentes.

Primeiro, vamos tentar fazer uma conexão de um container **UBUNTU** com um container do _nginx_ **SEM UTILIZAR NETWORK**. Nesse caso vamos fazer uma requisição e aguardar uma resposta.

**IMPORTANTE:** Quando você cria um container e não passa uma network, ele por padrão é adicionado em uma rede do tipo **bridge**. A partir da configuração que essa rede padrão do Docker possui, os containers podem se comunicar entre si através de IPs, mas **não conseguem se resolver** pelo nome do container, que é algo que normalmente acontece quando você usa **redes personalizadas** do Docker.

Crie um container com a imagem do nginx:
```yaml
docker run -d --name nginx-container nginx
```

Criando um container Ubuntu:
```yaml 
docker run -it --name ubuntu-container ubuntu
```

Iniciamos o container de forma iterativa, podendo executar comandos dentro dele. Vamos então intalar o **curl** para enviar uma **requisição ao nginx** a partir dele:
```sh
apt update && apt install -y curl
```

Agora, **vamos fazer uma requisição** para o nginx executando o seguinte comando no **terminal do container ubuntu**:
```yaml
    curl nginx-container
```

Nosso container falhou ao realizar a requisição, retornando a seguinte mensagem: **curl: (6) Could not resolve host: nginx-container**

Como os containers _"não estão na mesma rede"_, o ubuntu não conseguiu resolver o container do nginx a partir de seu nome.

Deixe o terminal que estamos usando para interagir com o ubuntu aberto e **abra um novo** para rodarmos mais alguns comandos.

Vamos fazer o mesmo processo, agora adicionando eles em uma network do tipo **bridge**:
```yaml
    docker network create -d bridge network-tutorial
```

**Obs:** Caso não passemos _-d <tipo-da-network>_ no comando acima, a network por padrão é criada com o tipo **bridge**

Adicione o container do nginx à nossa network:
_(O container deve estar rodando para ser adicionado à uma network)_
```yaml
    docker network connect network-tutorial nginx-container
```
```yaml
    docker network connect network-tutorial ubuntu-container
```

Agora vamos tentar fazer a requisição novamente, **voltando ao terminal do ubuntu** e executando o seguinte comando:
```yaml
    curl nginx-container
```

Se tudo deu certo, você receberá uma mensagem do nginx! 🎉