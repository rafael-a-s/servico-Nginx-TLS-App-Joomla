# Serviço Nginx c/ TLS e Aplicação Joomla

## Descrição

Este repositório contém um arquivos projetados para facilitar a implantação dos seguintes requisitos, Servidor Nginx c/ Joomla 5.0.3 instalado e certificado auto-assinado c/ TLS 1.3 e tamanho de chave de 3096 bits.

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
Entre no dirétorio:
```bash
cd servico-Nginx-TLS-App-Joomla
```

### Iniciar os Serviços
Navegue até o diretório docker:
```bash
cd docker
```
Execute:
```bash
docker build -t meu-nginx-tls13 .
```
Isso irá construir a imagem do nginx com o certificado auto-assinado c/ TLS 1.3 e tamanho de chave de 3096 bits. Essa imagem será usada no docker-compose.yml.

Agora vamos subir nossos containers, usando o docker-compose, execute:
```bash
docker-compose up -d
```
### Acessar o Joomla
Após a inicialização dos serviços, acesse o Joomla através do navegador, apontando para o endereço IP ou domínio do servidor Nginx configurado.

https://localhost:8443/installation/index.php

### Estrutura de pastas

Aqui está a estrutura :

```
servico-Nginx-*/    # Pasta raiz
|- config/          # Configurações, php e nginx
|- docker/          # Arquivos docker
readme.md           # Leia-me
```

### Como foi criado o certificado auto-assinado

```yml
RUN openssl req -x509 -nodes -days 365 -newkey rsa:3096 -keyout /etc/ssl/private/nginx-selfsigned.key -out /etc/ssl/certs/nginx-selfsigned.crt -subj "/C=US/ST=Denial/L=Springfield/O=Dis/CN=localhost"
```