# ms-course

Projeto de estudo focado em arquitetura de microsserviços utilizando Java, Spring Boot, Docker e Spring Cloud.

## 🚀 Tecnologias utilizadas

* Java 11
* Spring Boot
* Spring Cloud
* Eureka Server
* Spring Cloud Gateway / Zuul
* OpenFeign
* OAuth2 + JWT
* Docker
* Maven
* H2 Database
* Config Server

---

# 📚 Arquitetura do Projeto

O projeto é composto por múltiplos microsserviços responsáveis por autenticação, descoberta de serviços, configuração centralizada e regras de negócio.

## Microsserviços

| Serviço               | Descrição                                   |
| --------------------- | ------------------------------------------- |
| `hr-eureka-server`    | Service Discovery com Eureka                |
| `hr-config-server`    | Configuração centralizada                   |
| `hr-oauth`            | Autenticação e autorização com OAuth2 e JWT |
| `hr-user`             | Gerenciamento de usuários                   |
| `hr-worker`           | Serviço de trabalhadores                    |
| `hr-payroll`          | Serviço de folha de pagamento               |
| `hr-api-gateway-zuul` | API Gateway                                 |

---

# 🐳 Docker

## Criar rede Docker

```bash
docker network create hr-net
```

---

# ⚙️ Build dos projetos

Executar em cada microsserviço:

```bash
mvn clean package -DskipTests
```

---

# 🐳 Criando as imagens Docker

Exemplo:

```bash
docker build -t hr-config-server:v1 .
```

Repita o processo para todos os microsserviços.

---

# ▶️ Executando os containers

## Config Server

```bash
docker run -d \
--name hr-config-server \
--network hr-net \
-p 8888:8888 \
hr-config-server:v1
```

## Eureka Server

```bash
docker run -d \
--name hr-eureka-server \
--network hr-net \
-p 8761:8761 \
hr-eureka-server:v1
```

## OAuth

```bash
docker run -d \
--name hr-oauth \
--network hr-net \
-P \
hr-oauth:v1
```

## Worker

```bash
docker run -d \
--name hr-worker \
--network hr-net \
-P \
hr-worker:v1
```

## Payroll

```bash
docker run -d \
--name hr-payroll \
--network hr-net \
-P \
hr-payroll:v1
```

---

# 🔐 Configurações importantes

## `bootstrap.properties`

```properties
spring.application.name=hr-oauth
spring.cloud.config.uri=http://hr-config-server:8888
management.endpoints.web.exposure.include=*
```

---

## `application.properties`

```properties
eureka.client.service-url.defaultZone=http://hr-eureka-server:8761/eureka
```

---

# 🔑 Variáveis utilizadas

```properties
jwt.secret=123456
oauth.client.name=myappname
oauth.client.secret=myappsecret
```

Essas propriedades podem ficar no Config Server.

---

# 📡 Endpoints úteis

## Eureka Dashboard

```bash
http://localhost:8761
```

## Config Server

```bash
http://localhost:8888
```

---

# 🛠️ Comandos úteis Docker

## Ver containers ativos

```bash
docker ps
```

## Ver logs

```bash
docker logs -f hr-oauth
```

## Ver containers da rede

```bash
docker network inspect hr-net
```

---

# 📌 Objetivo do Projeto

Este projeto foi desenvolvido para estudo de:

* Arquitetura de microsserviços
* Comunicação entre serviços
* Balanceamento de carga
* Service Discovery
* Configuração centralizada
* Segurança com OAuth2 e JWT
* Dockerização de aplicações Spring Boot

---

# 👨‍💻 Autor

Jefferson França

GitHub:

[JeffersonTeodoro GitHub](https://github.com/JeffersonTeodoro?utm_source=chatgpt.com)
