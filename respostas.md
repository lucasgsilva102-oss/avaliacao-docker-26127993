# Respostas da Avaliação

## Parte 1 · Dockerfile do portal

1. Qual imagem base você usou e qual o tamanho final da imagem do portal?

Usei a imagem `nginx:1.27-alpine`, que é uma imagem oficial do Nginx. O tamanho final da imagem foi o tamanho mostrado pelo comando `docker images` para a imagem `g0mesxl/agrovale-portal:1.0-26127993`.

2. Em qual pasta do container o Nginx procura os arquivos do site? Mostre o comando que você usou para conferir que o `index.html` está lá dentro.

O Nginx procura os arquivos do site na pasta `/usr/share/nginx/html/`.

Para conferir os arquivos dentro do container, usei:

```cmd
docker exec teste-portal ls /usr/share/nginx/html

Assim consegui verificar se o index.html estava dentro da pasta usada pelo Nginx.

Parte 2 · Docker Hub
3. Nome completo da imagem publicada e link público do repositório no Docker Hub.

A imagem publicada foi:

g0mesxl/agrovale-portal:1.0-26127993

Link do repositório:

https://hub.docker.com/r/g0mesxl/agrovale-portal

4. Por que o docker login foi feito com um token de acesso e não com a senha da conta?

Usei um token de acesso porque é uma forma mais segura de fazer o login no Docker Hub. Assim não precisei usar diretamente a senha da conta no terminal.

Parte 3 · Página de manutenção
5. Preencha uma linha por defeito encontrado.
#	Instrução	O que estava errado	O que eu vi acontecer	Como corrigi
1	A página deveria ser servida pelo Nginx	O Dockerfile não copiava os arquivos da página para a pasta do Nginx	A página não estava sendo servida corretamente	Adicionei COPY site/ /usr/share/nginx/html/
2	A página deveria funcionar na porta 80 do container	O Dockerfile não tinha EXPOSE 80	A porta do serviço não estava declarada na imagem	Adicionei EXPOSE 80
3	A imagem deveria ter identificação do responsável	O Dockerfile não tinha um LABEL de identificação	Não havia identificação do responsável pela imagem	Adicionei um LABEL com meu nome e matrícula
6. Qual a diferença entre -p 7042:80 e -p 80:7042 no docker run? Qual dos dois números é a porta do container?

O primeiro número é a porta do computador e o segundo é a porta do container.

Por exemplo, -p 7042:80 usa a porta 7042 do computador e encaminha para a porta 80 do container.

Já -p 80:7042 usa a porta 80 do computador e encaminha para a porta 7042 do container.

Então, a porta do container é sempre o número depois dos dois pontos.

Parte 4 · docker-compose.yml
7. No serviço blog, por que WORDPRESS_DB_HOST recebe db e não localhost?

Porque o WordPress e o banco de dados estão em containers diferentes.

No Docker Compose, db é o nome do serviço do MariaDB. Por isso o WordPress consegue encontrar o banco usando db:3306.

Se fosse usado localhost, o WordPress procuraria o banco dentro do próprio container dele.

8. Por que o serviço db não publica a porta 3306? Se precisar consultar o banco, como faz sem publicar a porta? Mostre o comando.

A porta 3306 não foi publicada porque o WordPress consegue acessar o MariaDB pela rede interna do Docker Compose usando o nome db.

Para consultar o banco sem publicar a porta, posso entrar no container do MariaDB com:

docker exec -it <nome-do-container-db> mariadb -u agrovale -p
Parte 5 · Persistência
9. Quais comandos você usou para derrubar e subir a stack? Qual comando teria apagado o post que você criou, e por quê?

Para derrubar a stack usei:

docker compose down

Depois subi novamente com:

docker compose up -d

O comando que poderia apagar o post seria:

docker compose down -v

Isso acontece porque o -v remove os volumes. Como os dados do WordPress ficam armazenados no volume, remover o volume poderia apagar os dados do site, incluindo o post.

10. Código de conclusão impresso pelo verificador:

AGROVALE-26127993-3F7CDC65


### ⚠️ Só uma coisa

Na **questão 1**, ainda falta o **tamanho exato da imagem**. Não vou inventar esse número.

Depois de colar o texto acima, rode no CMD:

```cmd
docker images g0mesxl/agrovale-portal:1.0-26127993