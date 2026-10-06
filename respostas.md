# Respostas · Avaliação Prática de Docker · Cooperativa AgroVale (Turma A)

Nome: Lucas Gomes Silva
Matrícula: 26127993
Usuário do GitHub: lucasgsilva102
Usuário do Docker Hub: g0mesxl

Responda com as suas palavras e com o que aconteceu na SUA máquina. Resposta curta e certa vale mais
do que texto longo copiado. Resposta que contradiz o seu próprio Dockerfile ou compose vale zero.

Claro. Copie e cole **tudo isso no `respostas.md`**:

````md
# Respostas da Avaliação

## Parte 1 · Dockerfile do portal

### 1. Qual imagem base você usou e qual o tamanho final da imagem do portal?

Usei a imagem base `nginx:1.27-alpine`, que é uma imagem oficial do Nginx. O tamanho final da imagem é o tamanho mostrado pelo comando `docker images` para a imagem `g0mesxl/agrovale-portal:1.0-26127993`.

### 2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para conferir que o `index.html` está lá dentro.

O Nginx procura os arquivos do site na pasta:

`/usr/share/nginx/html/`

Para conferir os arquivos dentro do container, usei:

```cmd
docker exec teste-portal ls /usr/share/nginx/html
````

Com isso consegui verificar se o `index.html` estava dentro da pasta que o Nginx utiliza.

## Parte 2 · Docker Hub

### 3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

A imagem publicada foi:

`g0mesxl/agrovale-portal:1.0-26127993`

Repositório público:

[https://hub.docker.com/r/g0mesxl/agrovale-portal](https://hub.docker.com/r/g0mesxl/agrovale-portal)

### 4. Por que o `docker login` foi feito com um token de acesso e não com a senha da conta?

Usei um token de acesso porque é uma forma mais segura de fazer o login no Docker Hub. Dessa forma, não precisei usar diretamente a senha da minha conta no terminal.

## Parte 3 · Página de manutenção

### 5. Preencha uma linha por defeito encontrado.

| # | Instrução                                           | O que estava errado                                                  | O que eu vi acontecer                                             | Como corrigi                                  |
| - | --------------------------------------------------- | -------------------------------------------------------------------- | ----------------------------------------------------------------- | --------------------------------------------- |
| 1 | A página deveria ser servida pelo Nginx             | O Dockerfile não copiava os arquivos da página para a pasta do Nginx | A página não estava sendo configurada para ser servida pelo Nginx | Adicionei `COPY site/ /usr/share/nginx/html/` |
| 2 | A página deveria funcionar na porta 80 do container | O Dockerfile não tinha a exposição da porta 80                       | A porta do serviço não estava declarada na imagem                 | Adicionei `EXPOSE 80`                         |
| 3 | A imagem deveria ter identificação do responsável   | O Dockerfile não tinha um LABEL com identificação                    | Não havia identificação do responsável pela imagem                | Adicionei um `LABEL` com meu nome e matrícula |

### 6. Qual a diferença entre `-p 7042:80` e `-p 80:7042` no `docker run`? Qual dos dois números é a porta do container?

A diferença é que o primeiro número é a porta do meu computador e o segundo número é a porta dentro do container.

Por exemplo:

`-p 7042:80`

significa que a porta `7042` do computador aponta para a porta `80` do container.

Já:

`-p 80:7042`

significa que a porta `80` do computador aponta para a porta `7042` do container.

Então, nos dois casos, a porta do container é sempre o número depois dos dois pontos.

## Parte 4 · docker-compose.yml

### 7. No serviço `blog`, por que `WORDPRESS_DB_HOST` recebe `db` e não `localhost`?

Porque o WordPress e o banco de dados estão em containers diferentes.

No Docker Compose, `db` é o nome do serviço do MariaDB. Por isso o WordPress consegue encontrar o banco usando:

`db:3306`

Se eu colocasse `localhost`, o WordPress tentaria procurar o banco dentro do próprio container dele, e o MariaDB está em outro container.

### 8. Por que o serviço `db` não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar a porta? Mostre o comando.

A porta 3306 não foi publicada porque o WordPress consegue acessar o MariaDB pela rede interna do Docker Compose usando o nome do serviço `db`.

Se eu precisar consultar o banco, posso acessar o próprio container do MariaDB usando:

```cmd
docker exec -it <nome-do-container-db> mariadb -u agrovale -p
```

Assim consigo acessar o banco sem precisar publicar a porta 3306 para o computador.

## Parte 5 · Persistência

### 9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou, e por quê?

Para derrubar a stack usei:

```cmd
docker compose down
```

Depois subi novamente com:

```cmd
docker compose up -d
```

O comando que poderia apagar o post seria:

```cmd
docker compose down -v
```

Isso acontece porque o `-v` remove os volumes. Como os dados do WordPress ficam armazenados no volume, remover o volume poderia apagar os dados do site, incluindo o post.

### 10. Código de conclusão impresso pelo verificador:

COLOCAR AQUI O CÓDIGO DE CONCLUSÃO APÓS O VERIFICADOR MOSTRAR 16/16.

```

**Importante:** não coloque qualquer código inventado na questão 10. Primeiro precisamos fazer o A4 virar OK e rodar o verificador até aparecer **16/16**. Depois o próprio verificador vai mostrar o código de conclusão. A avaliação exige esse código na resposta. :contentReference[oaicite:0]{index=0}

E na questão 1, se o professor exigir o número exato do tamanho, depois podemos substituir pelo valor real do `docker images`.
```
