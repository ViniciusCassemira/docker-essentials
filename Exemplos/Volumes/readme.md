# Usando volumes na prática

Vamos ver um exemplo prático do uso e funcionamento dos dois tipos de volumes, **volumes nomeados** e os **volumes anônimos**.
Em nosso exemplo, vamos instanciar um container a partir da **imagem oficial do mysql** e ver como os volumes se comportam.

## Volumes nomeados

Comece criando um volume nomeado, vamos usá-lo para a salvar e persistir os dados que desejamos. Nesse caso, nosso volume se chamará **db-volume**
```sh
    docker volume create db-volume
```

Agora, vamos criar um container a partir da imagem **mysql** chamado **meu-banco**, passando para esse container o volume que ele deverá utilizar para a persistência dos dados.

```sh
    docker container run -d --name meu-banco -v db-volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=senha1234 mysql
```

Agora que nosso container está criado, vamos falar para o Docker executar alguns comandos dentro dele
```sh
    docker container exec -it meu-banco /bin/bash
```

Vamos logar no mysql com o usuário root _(-u root)_ com a senha **senha1234** que definimos _(-p)_.
**Obs:** Não passe a senha como parâmetro, você deve inserir ela **depois** do seguinte comando:
```sh
    mysql -u root -p
```

Vamos criar um banco de dados para fazer o nosso teste, vou chamá-lo de **usuarios** 
```sh
    create database usuarios;
```

Para sair do nosso container, aperte as teclas **CTRL** + **D** até voltar para o seu terminal.

Peça para o docker **parar a execução do container** criado:
```sh
    docker container stop meu-banco
```

**Exclua** o container que acabamos de parar:
```sh
    docker container rm meu-banco
```

Apagamos o nosso container, mas suas informações ficaram salvas no volume, pois nosso volume **não foi apagado**. Vou criar **um novo container** nomeando ele como **novo-banco**, referenciando o mesmo volume em seu diretório _/var/lib/mysql_:
```sh
        docker container run -d --name novo-banco -v db-volume:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=senha1234 mysql
```

Vamos conferir se nosso banco **usuarios** ficou salvo. Vamos entrar nesse container para acessar o mysql.
```sh
    docker container exec -it novo-banco /bin/bash
```

Acesse o mysql (não se esqueça de usar a senha corretamente)
```sh
    mysql -u root -p
```

Vamos pedir para o mysql mostrar os **databases** existentes:
```sh
    show databases;
```

Se a base de dados **usuários** aparecer, significa que nosso volume armazenou as informações corretamente! 🎉

## Volumes anônimos

Diferente dos volumes nomeados, os **volumes anônimos** são criados automaticamente pelo Docker quando especificamos um volume sem nome. Vamos testar como eles funcionam.

Crie um container com um volume anônimo:
```sh
docker container run -d --name banco-anonimo -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=senha1234 mysql
```

Agora, entre no container e acesse o MySQL:
```sh
docker container exec -it banco-anonimo /bin/bash
```

Acesse o MySQL:
```sh
mysql -u root -p
```

Crie um banco de dados de teste:
```sql
CREATE DATABASE anon_db;
```

Saia do container e remova-o:
```sh
docker container stop banco-anonimo
docker container rm banco-anonimo
```

Agora, crie um novo container e veja se o banco **anon_db** ainda está lá:
```sh
docker container run -d --name novo-anonimo -v /var/lib/mysql -e MYSQL_ROOT_PASSWORD=senha1234 mysql
```

Entre no container e liste os bancos:
```sh
docker container exec -it novo-anonimo /bin/bash
mysql -u root -p
SHOW DATABASES;
```

Diferente do volume nomeado, o banco **anon_db** **não será encontrado**, pois os volumes anônimos são recriados a cada novo container. Isso demonstra que volumes anônimos **não** garantem persistência de dados entre containers diferentes.