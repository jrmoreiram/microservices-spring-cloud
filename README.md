# Microservices com Spring Cloud

Curso prático sobre arquitetura de microserviços utilizando **Spring Cloud**, cobrindo registro de serviços, centralização de configurações e rastreamento distribuído.

**Descrição:** Registry, Config Server e Distributed Tracing

---

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Temas Abordados](#temas-abordados)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Arquitetura do Sistema](#arquitetura-do-sistema)
- [Pré-requisitos](#pré-requisitos)
- [Instalação e Configuração](#instalação-e-configuração)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Microserviços](#microserviços)
- [Guia de Uso](#guia-de-uso)
- [Configuração Avançada](#configuração-avançada)
- [Monitoramento e Observabilidade](#monitoramento-e-observabilidade)
- [APIs REST](#apis-rest)
- [Troubleshooting](#troubleshooting)
- [Boas Práticas](#boas-práticas)
- [Contribuindo](#contribuindo)
- [Licença](#licença)

---

## 🎯 Sobre o Projeto

Este projeto é um repositório de aprendizado que demonstra as principais práticas e padrões de desenvolvimento de microserviços com o ecossistema **Spring Cloud**. Implementa uma arquitetura completa com descoberta de serviços, gerenciamento centralizado de configurações e rastreamento distribuído para melhorar a observabilidade e manutenibilidade de sistemas distribuídos.

### Objetivos de Aprendizado

- Entender a decomposição de arquiteturas monolíticas em serviços independentes
- Implementar padrões de service discovery com Eureka
- Centralizar gerenciamento de configurações com Spring Config Server
- Aplicar load balancing client-side com Ribbon
- Implementar observabilidade com distributed tracing (Sleuth + Zipkin)
- Comunicação entre serviços via REST com Feign
- Resiliência e circuit breaker com Hystrix

---

## 🔍 Temas Abordados

- ✅ Decomposição do monólito em microserviços
- ✅ Service Discovery com Eureka Server
- ✅ Centralização de configurações com Spring Config Server
- ✅ Disponibilidade com Client-side Load Balancer (Ribbon)
- ✅ Monitoramento e depuração com Distributed Tracing (Sleuth)
- ✅ Visualização de traces com Zipkin
- ✅ Comunicação declarativa com Feign Client
- ✅ Resiliência com Circuit Breaker (Hystrix)
- ✅ Logging centralizado e correlação de requisições

---

## 🛠️ Tecnologias Utilizadas

| Tecnologia | Versão | Descrição |
|-----------|--------|-----------|
| Java | 11+ | Linguagem de programação |
| Spring Boot | 2.x+ | Framework base para aplicações web |
| Spring Cloud | 2021.x+ | Ecossistema de microserviços |
| Eureka Server | 2.x | Service Discovery e Registry |
| Config Server | 2.x | Gerenciamento centralizado de configurações |
| Spring Feign | 2.x | Cliente HTTP declarativo |
| Spring Sleuth | 2.x | Rastreamento distribuído |
| Zipkin | 2.x+ | Visualização e análise de traces |
| Ribbon | 2.x | Load Balancer client-side |
| Maven | 3.6+ | Gerenciador de dependências e build |
| Git | 2.x+ | Controle de versão |
| Docker | 20.x+ | Containerização (opcional) |

---

## 🏗️ Arquitetura do Sistema

### Visão Geral

A arquitetura segue o padrão de microserviços com componentes centralizados:

```
┌─────────────────────────────────────────────────────────────────┐
│                         Cliente / API Gateway                   │
└──────────────┬──────────────────────────────────────────────────┘
               │
        ┌──────┴──────┐
        │             │
   ┌────▼────┐  ┌────▼────┐
   │  Loja   │  │Fornecedor│
   │ Service │  │ Service  │
   └────┬────┘  └────┬────┘
        │             │
        └──────┬──────┘
               │
        ┌──────▼──────────────┐
        │   Eureka Server     │
        │ (Service Registry)  │
        └─────────────────────┘
               │
        ┌──────▼──────────────┐
        │  Config Server      │
        │ (Centralized Config)│
        └─────────────────────┘
               │
        ┌──────▼──────────────┐
        │  Zipkin Server      │
        │ (Distributed Tracing│
        │   & Monitoring)     │
        └─────────────────────┘
```

### Componentes Principais

1. **Eureka Server**: Servidor de descoberta de serviços que mantém um registro de todos os microserviços disponíveis
2. **Config Server**: Centraliza as configurações de todos os serviços em um repositório Git
3. **Microserviços**: Serviços de negócio (Loja, Fornecedor) que se registram no Eureka
4. **Zipkin Server**: Coleta e visualiza traces distribuídos de todas as requisições

---

## 📦 Pré-requisitos

Antes de começar, certifique-se de ter instalado:

- **Java Development Kit (JDK) 11** ou superior
  - Verificar: `java -version`
- **Maven 3.6+** ou **Gradle 7+**
  - Verificar: `mvn -version`
- **Git 2.x+**
  - Verificar: `git --version`
- **Docker 20.x+** (opcional, mas recomendado)
  - Verificar: `docker --version`

### Requisitos de Sistema

- **RAM mínima**: 4GB (recomendado 8GB)
- **Espaço em disco**: 2GB disponível
- **Portas necessárias**: 8761, 8888, 9411, 8081, 8082

---

## 🚀 Instalação e Configuração

### 1. Clone o Repositório

```bash
git clone https://github.com/jrmoreiram/microservices-spring-cloud.git
cd microservices-spring-cloud
```

### 2. Estrutura Esperada após o Clone

```
microservices-spring-cloud/
├── eureka-server/          # Servidor de descoberta de serviços
├── config-server/          # Servidor de configurações centralizado
├── loja/                   # Microserviço de loja
├── fornecedor/             # Microserviço de fornecedor
├── pom.xml                 # POM do projeto pai (multi-módulo)
└── README.md               # Este arquivo
```

### 3. Build do Projeto

#### Opção A: Build Completo

```bash
# Build de todos os módulos
mvn clean install

# Ou com skip de testes
mvn clean install -DskipTests
```

#### Opção B: Build de um Módulo Específico

```bash
# Build apenas do Eureka Server
mvn clean install -pl eureka-server

# Build apenas do Config Server
mvn clean install -pl config-server

# Build apenas do microserviço Loja
mvn clean install -pl loja
```

### 4. Execução dos Serviços

Abra múltiplos terminais e inicie os serviços na ordem indicada:

#### Terminal 1: Eureka Server

```bash
cd eureka-server
mvn spring-boot:run
```

**Esperado**: Aplicação inicia em `http://localhost:8761`

#### Terminal 2: Config Server

```bash
cd config-server
mvn spring-boot:run
```

**Esperado**: Aplicação inicia em `http://localhost:8888`

#### Terminal 3: Microserviço Fornecedor

```bash
cd fornecedor
mvn spring-boot:run
```

**Esperado**: Aplicação inicia em `http://localhost:8081` (porta configurável)

#### Terminal 4: Microserviço Loja

```bash
cd loja
mvn spring-boot:run
```

**Esperado**: Aplicação inicia em `http://localhost:8082` (porta configurável)

#### Terminal 5: Zipkin (Rastreamento Distribuído)

```bash
# Opção 1: Docker (recomendado)
docker run -d -p 9411:9411 openzipkin/zipkin:latest

# Opção 2: Jar standalone
java -jar zipkin.jar
```

**Esperado**: Zipkin disponível em `http://localhost:9411`

---

## 📁 Estrutura do Projeto

### Eureka Server

```
eureka-server/
├── src/main/java/
│   └── EurekaServerApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── application.yml
└── pom.xml
```

**Configuração padrão**:
- Porta: 8761
- URL: http://localhost:8761

### Config Server

```
config-server/
├── src/main/java/
│   └── ConfigServerApplication.java
├── src/main/resources/
│   └── application.properties
├── config/
│   ├── loja-development.properties
│   ├── loja-production.properties
│   ├── fornecedor-development.properties
│   └── fornecedor-production.properties
└── pom.xml
```

**Configuração padrão**:
- Porta: 8888
- URL base: http://localhost:8888

### Microserviços (Loja e Fornecedor)

```
loja/
├── src/main/java/
│   ├── Loja.java
│   ├── controller/
│   ├── service/
│   ├── client/
│   └── LojaMicroserviceApplication.java
├── src/main/resources/
│   ├── application.properties
│   └── application.yml
└── pom.xml
```

---

## 🔧 Microserviços

### 1. Eureka Server (Service Registry)

**Responsabilidade**: Mantém o registro dinâmico de todos os microserviços

**Configuração mínima** (application.yml):
```yaml
server:
  port: 8761

eureka:
  server:
    enable-self-preservation: true
  client:
    register-with-eureka: false
    fetch-registry: false
```

**Acesso**: http://localhost:8761

### 2. Config Server (Centralized Configuration)

**Responsabilidade**: Fornece configurações centralizadas baseadas em Git

**Configuração mínima** (application.properties):
```properties
server.port=8888
spring.cloud.config.server.git.uri=https://github.com/seu-usuario/config-repo.git
spring.cloud.config.server.git.username=seu-usuario
spring.cloud.config.server.git.password=seu-token
```

**Endpoints de configuração**:
- `GET /loja/default` - Configuração padrão
- `GET /loja/development` - Configuração de desenvolvimento
- `GET /loja/production` - Configuração de produção

### 3. Microserviço Loja

**Responsabilidade**: Gerenciar operações de loja

**Configuração mínima** (application.yml):
```yaml
server:
  port: 8082

spring:
  cloud:
    config:
      uri: http://localhost:8888
    discovery:
      client:
        serviceUrl:
          defaultZone: http://localhost:8761/eureka

eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka
  instance:
    preferIpAddress: true
```

### 4. Microserviço Fornecedor

**Responsabilidade**: Gerenciar operações de fornecedor

**Configuração similar ao Loja, ajustando**:
- `server.port: 8081`
- `spring.application.name: fornecedor`

---

## 📖 Guia de Uso

### Verificando o Status dos Serviços

#### Eureka Dashboard

Acesse: http://localhost:8761

Você deve ver os serviços registrados:
- `FORNECEDOR`
- `LOJA`

### Consultando Configurações

```bash
# Configuração padrão de Loja
curl http://localhost:8888/loja/default

# Configuração de desenvolvimento
curl http://localhost:8888/loja/development

# Configuração de produção
curl http://localhost:8888/loja/production
```

### Rastreamento de Requisições

1. Acesse o dashboard do Zipkin: http://localhost:9411
2. Selecione um serviço na dropdown
3. Clique em "Find Traces"
4. Visualize os traces de requisições distribuídas

---

## ⚙️ Configuração Avançada

### Configurar Profiles de Ambiente

#### Development (application-dev.yml)

```yaml
spring:
  profiles: dev
  cloud:
    config:
      uri: http://localhost:8888

logging:
  level:
    root: INFO
    com.seu-projeto: DEBUG
```

#### Production (application-prod.yml)

```yaml
spring:
  profiles: prod
  cloud:
    config:
      uri: http://config-server.producao.com:8888

logging:
  level:
    root: WARN
    com.seu-projeto: INFO
```

### Executar com Profile Específico

```bash
# Development
mvn spring-boot:run -Dspring-boot.run.arguments="--spring.profiles.active=dev"

# Production
mvn spring-boot:run -Dspring-boot.run.arguments="--spring.profiles.active=prod"
```

### Habilitando Sleuth para Tracing

```yaml
spring:
  sleuth:
    sampler:
      probability: 1.0  # Trace todas as requisições
    trace-id128: true
    web:
      skip-pattern: (^metrics.*|^health.*|^info.*)
  zipkin:
    base-url: http://localhost:9411
```

---

## 📊 Monitoramento e Observabilidade

### Spring Sleuth - Distributed Tracing

O Sleuth adiciona automaticamente:
- **Trace ID**: Identificador único para a requisição completa
- **Span ID**: Identificador único para cada operação

**Exemplo de log com Sleuth**:
```
[loja,d1b0d1e72d4e5bc0,d1b0d1e72d4e5bc0,true] 2023-01-15 10:30:45
```

Onde:
- `loja`: Nome da aplicação
- `d1b0d1e72d4e5bc0`: Trace ID
- `d1b0d1e72d4e5bc0`: Span ID
- `true`: Enviado para Zipkin

### Zipkin - Visualização de Traces

**Acessar**: http://localhost:9411

**Recursos**:
- Visualizar requisições entre serviços
- Identificar gargalos de performance
- Analisar latência por serviço
- Exportar traces em diferentes formatos

### Métricas com Actuator

**Habilitar no microserviço**:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

**Endpoints disponíveis**:
- `GET /actuator/health` - Status da aplicação
- `GET /actuator/metrics` - Métricas disponíveis
- `GET /actuator/env` - Variáveis de ambiente

---

## 🔌 APIs REST

### Microserviço Fornecedor

#### Listar Fornecedores

```bash
curl -X GET http://localhost:8081/fornecedores \
  -H "Content-Type: application/json"
```

**Response** (200 OK):
```json
[
  {
    "id": 1,
    "nome": "Fornecedor A",
    "cnpj": "12.345.678/0001-00",
    "contato": "contato@fornecedora.com"
  }
]
```

#### Obter Fornecedor por ID

```bash
curl -X GET http://localhost:8081/fornecedores/1 \
  -H "Content-Type: application/json"
```

### Microserviço Loja

#### Listar Produtos

```bash
curl -X GET http://localhost:8082/produtos \
  -H "Content-Type: application/json"
```

#### Consultar Fornecedor (Comunicação Entre Serviços)

```bash
curl -X GET http://localhost:8082/consulta-fornecedor/1 \
  -H "Content-Type: application/json"
```

**Nota**: Esta chamada é feita via Feign Client e passa pelo Eureka

---

## 🐛 Troubleshooting

### Problema: Serviço não aparece no Eureka

**Causas Possíveis**:
1. Eureka Server não está rodando
2. URL do Eureka está incorreta na configuração

**Solução**:
```bash
# Verificar se Eureka está rodando
curl http://localhost:8761

# Verificar configuração no microserviço
# application.yml deve conter:
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka
```

### Problema: Config Server não retorna configurações

**Causas Possíveis**:
1. Repositório Git não é acessível
2. Credenciais de acesso incorretas
3. Arquivo de configuração não existe

**Solução**:
```bash
# Testar conectividade com Config Server
curl http://localhost:8888/loja/default

# Verificar logs do Config Server
# Deve haver mensagens sobre clone do repositório Git
```

### Problema: Traces não aparecem no Zipkin

**Causas Possíveis**:
1. Zipkin não está rodando
2. Sleuth não está habilitado corretamente
3. Taxa de amostragem é 0

**Solução**:
```yaml
# application.yml
spring:
  sleuth:
    sampler:
      probability: 1.0  # Garantir que traces sejam enviados
  zipkin:
    base-url: http://localhost:9411
```

### Problema: Porta já está em uso

**Solução**:
```bash
# Listar processo usando porta (Linux/Mac)
lsof -i :8761

# Matar processo
kill -9 <PID>

# Ou mudar porta em application.properties
server.port=8791
```

### Problema: Erro de Classe não encontrada

**Solução**:
```bash
# Limpar cache Maven
mvn clean

# Baixar dependências novamente
mvn install -DskipTests
```

---

## ✨ Boas Práticas

### 1. Versionamento de APIs

```java
@RestController
@RequestMapping("/api/v1/produtos")
public class ProdutoControllerV1 {
    // Implementação
}
```

### 2. Circuit Breaker (Resiliência)

```java
@Service
public class FornecedorService {
    
    @HystrixCommand(
        fallbackMethod = "fornecedorPadraoFallback",
        commandProperties = {
            @HystrixProperty(name = "execution.isolation.thread.timeoutInMilliseconds", value = "2000")
        }
    )
    public Fornecedor buscarFornecedor(Long id) {
        return fornecedorClient.buscar(id);
    }
    
    public Fornecedor fornecedorPadraoFallback(Long id) {
        return new Fornecedor("Fornecedor Padrão");
    }
}
```

### 3. Logging Estruturado

```java
@Slf4j
@Service
public class LojaService {
    
    public void processarPedido(Long pedidoId) {
        log.info("Processando pedido: {}", pedidoId);
        try {
            // Lógica de negócio
            log.debug("Pedido processado com sucesso");
        } catch (Exception e) {
            log.error("Erro ao processar pedido: {}", pedidoId, e);
        }
    }
}
```

### 4. Health Checks

```java
@Component
public class CustomHealthIndicator implements HealthIndicator {
    
    @Override
    public Health health() {
        // Verificar algum recurso crítico
        if (isResourceAvailable()) {
            return Health.up().withDetail("recurso", "disponível").build();
        }
        return Health.down().withDetail("recurso", "indisponível").build();
    }
    
    private boolean isResourceAvailable() {
        // Lógica de verificação
        return true;
    }
}
```

### 5. Documentação com Swagger/Springdoc

```xml
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.0.0</version>
</dependency>
```

Acessar: http://localhost:8082/swagger-ui.html

---

## 👥 Contribuindo

Contribuições são bem-vindas! Siga os passos abaixo:

1. **Fork o repositório**
   ```bash
   git clone https://github.com/seu-usuario/microservices-spring-cloud.git
   cd microservices-spring-cloud
   ```

2. **Crie uma branch para sua feature**
   ```bash
   git checkout -b feature/minha-feature
   ```

3. **Commit suas mudanças**
   ```bash
   git commit -m "Adicionar minha feature"
   ```

4. **Push para a branch**
   ```bash
   git push origin feature/minha-feature
   ```

5. **Abra um Pull Request**
   - Descreva suas alterações
   - Referencie issues relacionadas

### Diretrizes de Contribuição

- Seguir o padrão de código existente
- Adicionar testes unitários
- Atualizar documentação
- Respeitar o gitflow

---

## 📄 Licença

Este projeto está licenciado sob a licença **MIT** - veja o arquivo LICENSE para detalhes.

---

## 📚 Recursos Adicionais

- [Spring Cloud Documentation](https://spring.io/projects/spring-cloud)
- [Eureka Documentation](https://github.com/Netflix/eureka)
- [Zipkin Documentation](https://zipkin.io/)
- [Spring Boot Actuator](https://spring.io/guides/gs/actuator-service/)

---

## ❓ Dúvidas ou Sugestões?

Abra uma [Issue](https://github.com/jrmoreiram/microservices-spring-cloud/issues) ou entre em contato através de discussões.

---

**Última atualização**: 2026-03-28 13:46:54