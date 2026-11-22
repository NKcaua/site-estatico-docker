# Site estático com Docker (P2)

Projeto da disciplina: containerização de um site estático (HTML, CSS, JS e imagem) usando Docker e Nginx.

## Estrutura do projeto

```
.
├── Dockerfile
├── index.html
├── style.css
├── script.js
└── img/
    └── foto.png
```

## Pré-requisito

Ter o Docker instalado e em execução:

```bash
docker --version
```

## Dockerfile

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```

- `FROM nginx:alpine`: usa como base a imagem leve do servidor web Nginx.
- `COPY . /usr/share/nginx/html`: copia os arquivos do site para a pasta de onde o Nginx serve as páginas.
- `EXPOSE 80`: documenta que o container usa a porta 80.

## Build da imagem

Na raiz do projeto (onde está o `Dockerfile`):

```bash
docker build -t site-estatico .
```

## Executar o container

```bash
docker run -d --name meu-site -p 8080:80 site-estatico
```

- `-d`: executa em segundo plano.
- `--name meu-site`: dá um nome ao container.
- `-p 8080:80`: mapeia a porta 8080 do computador para a porta 80 do container.

Para conferir que está rodando:

```bash
docker ps
```

## Acessar o site

Abra no navegador: <http://localhost:8080>

## Parar e remover o container

```bash
docker stop meu-site
docker rm meu-site
```

## Atualizar o site após alterações

A imagem guarda uma cópia dos arquivos no momento do build. Ao alterar o site, é preciso refazer o build e recriar o container:

```bash
docker stop meu-site
docker rm meu-site
docker build -t site-estatico .
docker run -d --name meu-site -p 8080:80 site-estatico
```

## Diferença entre imagem e container

A **imagem** é como um molde ou uma receita pronta: um pacote somente leitura que contém o Nginx, as configurações e os arquivos do meu site. Ela é criada com o `docker build` a partir do Dockerfile e, sozinha, não executa nada.

O **container** é a imagem em execução, ou seja, uma instância viva criada com o `docker run`. A partir de uma mesma imagem posso criar vários containers, e apagar um container não apaga a imagem. Fazendo uma analogia: a imagem é o programa instalado e o container é o programa aberto rodando.

## Evidência de funcionamento

Vídeo mostrando o build, a execução do container e o site aberto no navegador em `http://localhost:8080`:

**Link do vídeo:** _(colar aqui o link ou o nome do arquivo)_

## Uso de IA

Este trabalho foi desenvolvido com o auxílio do **Claude** (Anthropic).
