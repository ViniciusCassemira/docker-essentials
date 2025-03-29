# Dockerfile 📄🐋

Um **Dockerfile** é um arquivo de texto que contém instruções para criar uma **imagem Docker**. Cada linha do arquivo define uma etapa do processo de construção do container. Abaixo estão as intruções mais comuns e seu uso:

## 📌 Pincipais instruções de um Dockerfile

### 1️⃣ `FROM` (Imagem base)
Define a imagem base para o container. Sendo sempre a primeira linha do `Dockerfile`.

```Dockerfile
FROM python:3.9-alpine
```
Esse comando usa a imagem **Python 3.9** baseada no **Alpine Linux** (uma versão leve do Linux).

---

### 2️⃣ `WORKDIR` (Diretório de trabalho)
Define o diretório onde os comandos serão executados dentro do seu container.

```Dockerfile
WORKDIR /app
```
Isso garante que qualquer comando `RUN`, `CMD` ou `COPY` seja executado dentro de `/app`.

---

### 3️⃣ `COPY` e `ADD` (Copiar arquivos para o container)
Esses comandos copiam arquivos do sistema host(máquina hospedeira) para dentro do container.

**Exemplo usando `COPY`**
```Dockerfile
COPY . /app
```
Isso copia todos os arquivos do diretório local para `/app` no container.

**Exemplo usando `ADD`** (permite baixar arquivos de URLs)
```Dockerfile
ADD https://example.com/file.tar.gz /app/
```
Isso baixa o arquivo diretamente para `/app/`.

---

### 4️⃣ `RUN` (Executar comandos no container)
Usado para executar comandos durante a **construção da imagem**.

```Dockerfile
RUN apt-get update && apt-get install -y curl
```
Isso instala o `curl` no container **durante a build**.

---

### 5️⃣ `CMD` vs. `ENTRYPOINT` (Comando padrão do container)
Define o comando que será executado quando o container iniciar.

**Exemplo de `CMD` (forma mais simples)**
```Dockerfile
CMD ["python", "app.py"]
```
Aqui, ao rodar o container, ele executará `python app.py`.

**Exemplo de `ENTRYPOINT` (mais flexível)**
```Dockerfile
ENTRYPOINT ["python"]
CMD ["app.py"]
```
Isso permite sobrescrever o comando ao rodar o container:

```sh
docker run minha-imagem outro_script.py
```

---

### 6️⃣ `EXPOSE` (Definir portas abertas no container)
Indica quais portas o container usará ao estar em funcionamento (mas não faz o redirecionamento).

```Dockerfile
EXPOSE 8080
```
Isso significa que a aplicação no container roda na porta `8080`, mas o redirecionamento para a máquina hospedeira deve ser feito no comando `docker run -p` ao criar um container.

---

### 7️⃣ `ENV` (Variáveis de ambiente)
Define variáveis de ambiente dentro do container.

```Dockerfile
ENV PORT=8080
```
Isso permite acessar a variável dentro do código da aplicação como `process.env.PORT` (Node.js) ou `os.getenv("PORT")` (Python).

---

### 8️⃣ `VOLUME` (Diretórios persistentes)
Cria um volume para persistência de dados.

```Dockerfile
VOLUME /data
```
Isso mantém os arquivos em `/data` mesmo após o container ser removido.

---

### 9️⃣ `ARG` (Passagem de argumentos na build)
Permite definir variáveis que podem ser passadas **durante a construção da imagem** (`docker build`).

```Dockerfile
ARG VERSAO_NODE=18
FROM node:${VERSAO_NODE}-alpine
```
Para construir a imagem com um Node.js diferente:
```sh
docker build --build-arg VERSAO_NODE=16 -t minha-imagem .
```

---

## 🎯 Exemplo Completo de Dockerfile
```Dockerfile
# Definir imagem base
FROM node:18-alpine

# Criar diretório de trabalho
WORKDIR /app

# Copiar arquivos para o container
COPY . .

# Instalar dependências
RUN npm install

# Definir variável de ambiente
ENV PORT=3000

# Expor porta
EXPOSE 3000

# Definir comando padrão
CMD ["node", "server.js"]