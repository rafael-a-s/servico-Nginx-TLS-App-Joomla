# Serviço Nginx c/ TLS e Aplicação Joomla

## Descrição

Este repositório contém um arquivo docker-compose.yml projetado para facilitar a implantação dos seguintes requisitos, Servidor Nginx c/ Joomla 5.0.3 instalado e certificado auto-assinado c/ TLS 1.3 e tamanho de chave de 3096 bits.

 - Servidor Nginx: Configurado para servir o Joomla na versão 5.0.3, oferecendo uma plataforma robusta e flexível para a criação de sites e aplicações web.
 - Segurança TLS: Inclui configuração para um certificado TLS auto-assinado com TLS 1.3, garantindo uma camada adicional de segurança através de criptografia. A chave utilizada tem um tamanho de 3096 bits, proporcionando uma forte proteção contra tentativas de descriptografia.

## Como Usar

### Pré-requisitos
    - Certifique-se de ter o Docker e o Docker Compose instalados em seu sistema.
### Clonar o repositório
clone este repositório para sua máquina local 
```bash
git clone https://github.com/rafael-a-s/servico-Nginx-TLS-App-Joomla.git
```

### Iniciar os Serviços
Navegue até o diretório contendo o docker-compose.yml e execute:

```bash
docker-compose up -d
```
### Acessar o Joomla
Após a inicialização dos serviços, acesse o Joomla através do navegador, apontando para o endereço IP ou domínio do servidor Nginx configurado.

### Estrutura de pastas

Aqui está a estrutura :

```
servico-Nginx-*/    # Pasta raiz
|- config/          # Configurações, php e nginx
|- docker/          # Arquivos docker
readme.md           # Leia-me
```

### Setup docker-compose.yml

```yml
--- services
    nginx:
        image: nginx:alpine
        restart: always
        ports:
            - 8080:80
        volumes:
            - ./joomla:/var/www/html
            - ./nginx.conf:/etc/nginx/nginx.conf
        depends_on:
            - joomla

    joomla:
        image: joomla:3.9.5-php7.3-fpm-alpine
        restart: always
        environment:
            - JOOMLA_DB_HOST=db
            - JOOMLA_DB_USER=postgres
            - JOOMLA_DB_PASSWORD=mysecretpassword
            - JOOMLA_DB_NAME=db
        volumes:
            - ./joomla:/var/www/html
            - ./makedb.php:/makedb.php
        depends_on:
            - db
---
--- banco de dados
    image: postgres:11.2-alpine
    restart: unless-stopped
    environment:
      - POSTGRES_DB=db
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=mysecretpassword
    volumes:
      - ./db:/var/lib/postgresql/data
---
```