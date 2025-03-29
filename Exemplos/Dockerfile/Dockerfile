# Definindo imagem base para o Dockerfile
FROM nginx:alpine

# Copiando todo o conteúdo do nosso projeto para a pasta ./usr/share/nginx/html
COPY . ./usr/share/nginx/html

# Quando uma container for criado a partir dessa imagem, ele exibirá na porta 80
EXPOSE 80