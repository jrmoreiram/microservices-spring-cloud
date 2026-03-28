# Microservices com Spring Cloud

Curso prático sobre arquitetura de microserviços utilizando **Spring Cloud**, cobrindo registro de serviços, centralização de configurações e rastreamento distribuído.

**Descrição:** Registry, Config Server e Distributed Tracing

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Temas Abordados](#temas-abordados)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Instalação](#instalação)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Aulas](#aulas)
- [Como Usar](#como-usar)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

---

## 🎯 Sobre o Projeto

Este projeto é um repositório de aprendizado que demonstra as principais práticas e padrões de desenvolvimento de microserviços com o ecossistema **Spring Cloud**.

### Objetivos de Aprendizado

- Entender a decomposição de arquiteturas monolíticas em serviços
- Implementar padrões de service discovery
- Centralizar gerenciamento de configurações
- Aplicar load balancing client-side
- Implementar observabilidade com distributed tracing

---

## 🔍 Temas Abordados

- ✅ Decomposição do monólito em microserviços
- ✅ Service Discovery com Eureka
- ✅ Centralização de configurações com Spring Config Server
- ✅ Disponibilidade com Client-side Load Balancer
- ✅ Monitoramento e depuração com Distributed Tracing

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Descrição |
|-----------|--------|-----------|
| Java | 11+ | Linguagem de programação |
| Spring Boot | 2.x+ | Framework base |
| Spring Cloud | 2021.x+ | Ecossistema de microserviços |
| Eureka | - | Service Discovery |
| Config Server | - | Gerenciamento centralizado de configurações |
| Spring Feign | - | Client HTTP declarativo |
| Spring Sleuth | - | Rastreamento distribuído |
| Zipkin | - | Visualização de traces |

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Java 11** ou superior
- **Maven 3.6+** ou **Gradle 7+**
- **Git**
- **Docker** (opcional, para executar Zipkin)

---

## 🚀 Instalação

### 1. Clone o Repositório

```bash
git clone https://github.com/jrmoreiram/microservices-spring-cloud.git
cd microservices-spring-cloud
