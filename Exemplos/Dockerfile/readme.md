# Exemplo de Dockerfile

Vamos criar uma **imagem** para o nosso projeto a partir de um **Dockerfile**.

Execute o seguinte comando dentro da pasta do **Dockerfile** para criar nossa imagem:
```sh
    docker build -t <nome-da-futura-imagem> .
```

Após gerar sua imagem, ela está pronta para ser usada. Vamos criar um container a partir dela para testar:
```sh
    docker run -d-p 8080:80 --name aplicacao <nome-da-imagem>
```