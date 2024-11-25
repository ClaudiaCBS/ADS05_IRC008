<div align="center">

# ADS05_IRC008

Repositório para apresentar o projeto desenvolvido para a disciplina Redes de Computadores do 5ADS da FATEC.

## <a href='http://lattes.cnpq.br/4723982029081265' target="Jean"> Prof. Jean Carlos Lourenço Costa </a>

# Criação de Infraestrutura de Rede para a Empresa XPTO

</div>

## :bookmark_tabs: Objetivo

Desenvolver uma infraestrutura de rede para a empresa fictícia XPTO, que atenda aos seguintes requisitos:
<br>

**1. Load Balancer:**
Implementar um sistema de balanceamento de carga utilizando, no mínimo, 3 máquinas para distribuir o tráfego.

**2. Proxy Reverso:**
Configurar uma máquina para atuar como proxy reverso, gerenciando as requisições dos usuários para os servidores apropriados.

**3. Banco de Dados:**
Implementar uma máquina dedicada para o banco de dados, garantindo a segurança e integridade dos dados.

**4. VPN:**
Configurar o acesso à rede através de uma VPN, garantindo que todas as comunicações sejam seguras.

**5. Docker:**
Utilizar o Docker para criar os servidores web e o banco de dados, garantindo portabilidade e fácil gestão dos serviços.

<br>

### :spiral_calendar: Data das Validações

| Validação |         Previsão de entrega          | Status                            |
| :-------: | :----------------------------------: | :-------------------------------- |
|    01     |       04/10/2024 - 08/10/2024        | :white_check_mark: Concluído      |
|    02     |       25/10/2024 - 29/10/2024        | :white_check_mark: Concluído      |
|    03     |       22/11/2024 - 26/11/2024        | :white_check_mark: Concluído      |
|    04     | 06/12/2024 - 10/12/2024 e 13/12/2024 | :construction: Em desenvolvimento |

# :rocket: Tecnologias Utilizadas

Para o desenvolvimento deste projeto foram utilizadas as seguintes ferramentas e tecnologias:

<table>
  <thead>
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/typescript/typescript-original.svg" alt="TypeScript" title="TypeScript" style="display: inline-block; margin: 0 auto; width: 60px">
    </th>
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg" alt="React" title="React" style="display: inline-block; margin: 0 auto; width: 60px"></th>
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nestjs/nestjs-original.svg" alt="NestJs" title="NestJs" style="display: inline-block; margin: 0 auto; width: 60px" />
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/mysql/mysql-original-wordmark.svg" alt="MySQL" title="MySQL" style="display: inline-block; margin: 0 auto; width: 60px" />
    </th>
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/ubuntu/ubuntu-original.svg" alt="Ubuntu" title="Ubuntu" style="display: inline-block; margin: 0 auto; width: 60px"/>
    </th>
    <th>
        <img src="https://cdn.jsdelivr.net/gh/devicons/devicon/icons/docker/docker-original.svg" alt="Docker" title="Docker" style="display: inline-block; margin: 0 auto; width: 60px">
    </th>
    <th>
        <img src="https://github.com/apiFatec/API-3-Semestre-Ionic/assets/112169639/8f7699b6-4ee3-4bfb-a761-f79faa45049d" alt="Tailwind" title="Tailwind" style="display: inline-block; margin: 0 auto; width: 60px">
    </th>
  </thead>

  <tbody>
    <td>Typescript</td>
    <td>React</td>
    <td>NestJs</td>
    <td>MySQL</td>
    <td>Ubuntu</td>
    <td>Docker</td>
    <td>Tailwind</td>
  </tbody>
</table>

# :rocket: Requisitos do Trabalho

## 1. Arquitetura da Rede

- Desenhar a topologia da rede, identificando as máquinas, conexões, e
  fluxos de dados.
- Detalhar o uso do load balancer, proxy reverso e banco de dados.

<p align="center">
      <img src="/docs/02_topologia_rede.png" alt="Topologia da Rede">

## 2. Configuração da Máquina Virtual na AWS

Para iniciar, foi criada uma instância dentro do **nível gratuito da AWS**, utilizando o sistema operacional **Ubuntu**. A configuração inicial seguiu os seguintes passos:

2.1. **Acesso ao AWS Management Console:**

- Primeiro, acessei o **AWS Management Console** e naveguei até a seção **EC2** (Elastic Compute Cloud).
- Em seguida, cliquei em **Launch Instance** para iniciar a criação de uma nova máquina virtual.

  2.2. **Atribuindo Nome e Tags:**

- Criei 3 máquinas virtuais com os seguintes nomes: frontEnd1 (onde está o projeto web), backEnd (onde está o Docker e o banco de dados) e loadBalance (onde está a configuração do Load Balancer, Proxy Reverso e VPN).

  2.3. **Escolha da Amazon Machine Image (AMI):**

- Selecionei a imagem **Ubuntu**, adequada para servidores Linux, garantindo que a instância fosse compatível com o **nível gratuito** da AWS.
- A instância escolhida foi a **t2.micro**, que oferece 1 vCPU e 1GB de memória RAM, ideal para pequenas aplicações e testes.

  2.4. **Key pair (login):**

- Para garantir uma conexão segura via SSH com a máquina virtual, a AWS utiliza um par de chaves criptográficas (Key Pair), composto por uma chave pública e uma chave privada. A chave pública é armazenada na instância, enquanto a chave privada é usada pelo usuário para autenticação.
- Para criar e configurar o Key Pair selecionei a opção Create new key pair para gerar um novo par de chaves, necessário para o login via SSH.
- Nome do par de chaves que estou usando neste projeto é chaveRedesAWS.
- Escolhi o tipo RSA, que é um padrão amplamente utilizado para criptografia e autenticação.
- Optei pelo formato PEM (Privacy Enhanced Mail), que é o formato necessário para se conectar via SSH em sistemas Unix/Linux e também compatível com algumas ferramentas no Windows.
- Após revisar as configurações, cliquei em Create key pair para gerar o arquivo da chave privada.
- Salvamento do arquivo chaveRedesAWS.pem e no meu sistema local. Esse arquivo será usado posteriormente para autenticar o login na instância AWS através do SSH.

  2.5. **Configuração de Rede:**

- Mantive as configurações de rede padrão da AWS, utilizando a **VPC (Virtual Private Cloud)** padrão e uma **subnet** disponível, assegurando que a instância tivesse acesso público para fins de conectividade.
- Selecionei as seguintes opções para permitir o tráfego de rede: HTTPS e HTTP.

  2.6. **Configuração de Armazenamento:**

- Configurei o volume de armazenamento em 8GB, utilizando o **EBS (Elastic Block Store)** com o tipo **General Purpose (SSD)**, garantindo um bom desempenho com baixo custo, ideal para um ambiente de desenvolvimento.

---

Com a instância devidamente configurada, ela está preparada para receber as aplicações e serviços que serão configurados posteriormente, como servidores web em containers Docker, banco de dados, VPN e demais componentes da infraestrutura de rede.

---

## 3. Bitvise

Com a instância configurada e acessível, instalei os seguintes serviços necessários:

3.1. **Servidor WWW – Apache:**

```cmd
sudo apt update
sudo apt install apache2
```

- Verificar o funcionamento acessando o endereço IPv4 público da instância:

```cmd
sudo systemctl status apache2
```

3.2. **Servidor de Banco de Dados – MySQL/MariaDB:**

```cmd
sudo apt install default-mysql-server
```

- Após a instalação, acessei o MySQL:

```cmd
sudo mysql -u root
```

- Adicionei uma senha para o usuário root e criei um banco de dados:

```cmd
 ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'senha-de-root';

 CREATE DATABASE nome-do-banco;

 exit;
```

3.3. **Outros Serviços:**

- **HTOP:** Para monitoramento de recursos.
  ```cmd
  sudo apt install htop
  ```
- **Net Tools:** Para ferramentas de rede essenciais.
  ```cmd
  sudo apt install net-tools
  ```
- **Git:** Para controle de versão e deploy da aplicação.
  ```cmd
  sudo apt install git
  ```
- **NodeJs:** Para rodar o JavaScript no backend.
  ```cmd
  sudo apt install nodejs
  ```
- **npm:** Para o gerenciamento de pacotes do Node.js.
  ```cmd
  sudo apt install npm
  ```
- **NestJs:** Para utilizar os comandos do NestJs no terminal.
  ```cmd
  npm i -g @nestjs/cli
  ```

## 4. Rodando o Projeto

### 4.1. Clonar o projeto

```cmd
git clone https://github.com/ClaudiaCBS/ADS05_IRC008.git
```

### 4.2. FrontEnd

- Verifique se a URL da API no arquivo api.tsx corresponde à URL pública da instância:

```cmd
sudo nano Projeto-de-Sistemas-Operacionais/frontend/src/services/api.tsx
```

- Edite conforme necessário:

```cmd
import axios from "axios";

const api = axios.create({baseURL : 'http://IPv4-público-da-instância:3000/'});

export default api
```

- Instalar as dependências do frontEnd.

```cmd
cd Projeto-de-Sistemas-Operacionais/frontend
npm install
nano node_modules/jwt-decode/build/esm/index.d.ts
```

- Adicionar ao arquivo:

```cmd
export interface JwtPayload {
    iss?: string;
    sub?: string;
    aud?: string[] | string;
    exp?: number;
    nbf?: number;
    iat?: number;
    jti?: string;
    role?: any;
}

```

- Liberar o módulo de reescrita do Apache:

```cmd
a2enmod rewrite
```

- Realizar o build do projeto:

```cmd
npm run build
```

- Configurar o Apache para servir o frontEnd:

```cmd
sudo mv Projeto-de-Sistemas-Operacionais/frontend/dist /var/www/
sudo nano /etc/apache2/sites-available/000-default.conf
```

- Editar o arquivo conforme abaixo:

```cmd
    <VirtualHost *:80>
      ServerAdmin webmaster@localhost
      DocumentRoot /var/www/html/seu-app-react/build

      <Directory /var/www/dist>
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted

        # Ativando a reescrita
        RewriteEngine On

        # Se o arquivo solicitado não existir, redireciona para o index.html
        RewriteCond %{REQUEST_FILENAME} !-f
        RewriteCond %{REQUEST_FILENAME} !-d
        RewriteRule ^ /index.html [L]
    </Directory>
  </VirtualHost>

```

- Criar o arquivo .htaccess na pasta /var/www/dist

```cmd
    <IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteBase /

    # Se o arquivo solicitado não existir, redireciona para o index.html
    RewriteCond %{REQUEST_FILENAME} !-f
    RewriteCond %{REQUEST_FILENAME} !-d
    RewriteRule ^ /index.html [L]
</IfModule>
```

- Reinicie o Apache para aplicar as configurações:

```cmd
    sudo systemctl restart apache2
```

### 4.3. BackEnd

- Instalar as dependências do backEnd:

```cmd
cd Projeto-de-Sistemas-Operacionais/backend
npm install
npm install --save @nestjs/typeorm typeorm mysql2

```

- Criar e configurar o arquivo .env:

```cmd
sudo touch .env
```

- Conteúdo:

```cmd
sudo nano .env
```

```cmd
DB_HOST=127.0.0.1
DB_PORT=3306
DB_USER=root
DB_PASSWORD=sua-senha
DATABASE=nome-do-banco-de-dados
TOKEN_JWT=coloque-qualquer-coisa
```

- Rodar o backEnd:

```cmd
nest start
```

## 5. Load Balancer e Proxy Reverso

- Instalar o NGINX:
  ```cmd
  sudo apt install nginx
  ```
- Criar o arquivo do Load Balance e Proxy Reverso na pasta /etc/nginx/conf.d/loadbalancer.conf

```cmd
  sudo nano /etc/nginx/conf.d/loadbalancer.conf
```

- Configurar o arquivo do Load Balance e Proxy Reverso:

```cmd
upstream frontend{
	server ip_publico1;
	server ip_publico2;
	server ip_publico3;
}

server {
	listen 80;


	location / {
		proxy_pass http://frontend;
	        proxy_set_header Host $host;
	        proxy_set_header X-Real-IP $remote_addr;
	        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	        proxy_set_header X-Forwarded-Proto $scheme;
	}

	        location ~* \.(css|js|png|jpg|jpeg|gif|ico)$ {
                proxy_pass http://frontend;
                proxy_set_header Host $host;
                proxy_set_header X-Real-IP $remote_addr;
                proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
                proxy_set_header X-Forwarded-Proto $scheme;
            }
}

```

- Reiniciar o NGINX para aplicar as configurações:

  ```cmd
  sudo systemctl restart nginx
  ```

## 6. Docker

Para este projeto, utilizei o Docker para configurar e gerenciar o banco de dados de forma prática e eficiente. Com o uso de contêineres, foi possível garantir a portabilidade e a facilidade na implantação, eliminando preocupações relacionadas à compatibilidade entre ambientes.  
A imagem oficial do **MySQL** foi utilizada para criar o contêiner do banco de dados. Todas as configurações, como nome do banco, usuário e senha, foram definidas no arquivo `docker-compose.yml`, permitindo uma inicialização automatizada e padronizada.

### 6.1. Instalar Docker e Docker Compose

```cmd
  sudo apt-get update
  sudo apt install docker.io -y
  sudo apt install docker-compose
```

### 6.2. Criar o arquivo docker compose

- Criar o arquivo `docker-compose.yml`

```cmd
  sudo vim docker-compose.yml
```

- Inserir as seguintes informações no arquivo `docker-compose.yml`

```cmd
version: '3.8'

services:
  mysql:
    image: mysql:8.0-oracle  # Imagem mais leve do mysql
    container_name: Mysql  # Nome do container
    environment:  # Váriaveis de ambiente mysql
      MYSQL_ROOT_PASSWORD: "fatec"  # Senha do usuário root (séra criado junto do container)
      MYSQL_USER: "root"  # Nome de usuário caso necessário
      MYSQL_PASSWORD: "fatec"  #  Senha para o usuário
      MYSQL_DATABASE: "redes"  # Nome para uma database
    ports:
      - "3306:3306"  # Porta do host e porta do container
    volumes:
      - mysql_data:/var/lib/mysql # Garante que os dados sejam persistentes

volumes:
  mysql_data:
```

### 6.3. Rodar o docker-compose

```cmd
  sudo docker-compose up -d
```

## 7. VPN

Para garantir a segurança na comunicação entre os servidores, foi configurada uma VPN (Rede Privada Virtual). A VPN cria um túnel criptografado entre os dispositivos conectados, permitindo o envio de dados de forma segura mesmo em redes públicas.
Neste projeto, a configuração foi feita utilizando OpenVPN na instância EC2 da AWS chamada loadbalance, que atua como o servidor VPN. A seguir estão as etapas para instalação e configuração.

### 7.1. Instalar VPN

```cmd
  sudo apt update
  sudo apt install openvpn
```

### 7.2. Configurar arquivos VPN

- Entrar na pasta openvpn.

```cmd
  cd /etc/openvpn
```

- Deletar as pastas padrão client e server.

```cmd
  rm -r client
  rm -r server
```

- Criar um arquivo para configuração do servidor.

```cmd
  sudo nano server1.conf
```

- Inserir as seguintes informações no arquivo `server1.conf`

```cmd
  ifconfig 192.168.0.100 192.168.0.200 # IP do servidor e IP do cliente
  remote 3.89.212.241 # IP público do Load Balance
  port 1194 # Porta do openvpn (pode ser qualquer outra)
  dev tun
  proto tcp-server
  secret chavevpn
  cipher AES256
  verb 4
  comp-lzo
  persist-key
  persist-tun
  keepalive 10 120
```

- Copiar o arquivo `server1.conf` para criar a configuração do cliente.

```cmd
  cat server1.conf > client1.conf
```

- Modificar o arquivo `client1.conf` para refletir a configuração do cliente.

```cmd
  ifconfig 192.168.0.200 192.168.0.100 # IP do cliente e IP do servidor
  remote 3.89.212.241 # IP público do Load Balance
  port 1194 # Porta do openvpn (pode ser qualquer outra)
  dev tun
  proto tcp-client
  secret chavevpn
  cipher AES256
  verb 4
  comp-lzo
  persist-key
  persist-tun
  keepalive 10 120
```

### 7.3. Criar chave criptografada

- Entrar na pasta openvpn.

```cmd
  cd /etc/openvpn
```

- Criar a chave VPN com o nome chavevpn

```cmd
  openvpn --genkey --secret chavevpn
```

- Garantir permissões de leitura e escrita para todos os usuários.

```cmd
  chmod 777 chavevpn
  chmod 777 client1.conf
```

### 7.4. Configurar segurança na AWS

- Acessar a instância EC2 na AWS.
- Em Security, adicionar uma regra ao grupo de segurança:
  - Tipo: Custom TCP
  - Porta: 1194
  - Origem: 0.0.0.0/0

### 7.5. Transferir arquivos para o cliente

- Fazer o download da chaveVPN e do arquivo de configuração do client1.conf.

```cmd
  scp -i <chaveRedesAWS.pem> ubuntu@3.89.212.241:/etc/openvpn/chavevpn /caminho/local/
  scp -i <chaveRedesAWS.pem> ubuntu@3.89.212.241:/etc/openvpn/client1.conf /caminho/local/
```

### 7.6. Iniciar o servidor VPN

- No servidor, iniciar o OpenVPN com o arquivo de configuração.

```cmd
  openvpn --config server1.conf
```
