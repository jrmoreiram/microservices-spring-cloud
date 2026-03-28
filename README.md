# Documentação do Projeto 

## Introdução 
Esta documentação fornece uma visão geral abrangente do projeto, abrangendo desde a configuração inicial até o desenvolvimento e contribuição. 

## Quick Start 
1. Clone o repositório: `git clone https://github.com/jrmoreiram/microservices-spring-cloud.git`
2. Navegue até o diretório do projeto: `cd microservices-spring-cloud`
3. Execute o comando de inicialização: `./mvnw spring-boot:run`.

## Visão Geral da Arquitetura 
O projeto é baseado na arquitetura de micro serviços, permitindo escabilidade e manutenção independente. Cada serviço é responsável por uma funcionalidade específica e se comunica através de APIs REST.

## Estrutura do Projeto 
- `src/main/java`: código-fonte dos serviços  
- `src/main/resources`: arquivos de configuração e templates  
- `src/test/java`: testes automatizados  

## Configuração 
A configuração dos serviços pode ser gerenciada através de arquivos `application.yml`. Certifique-se de ajustar as propriedades de conexão do banco de dados e variáveis de ambiente conforme necessário.

## Endpoints da API 
- `GET /api/servico`: Recupera todos os itens.  
- `POST /api/servico`: Cria um novo item.

## Executando Serviços 
Os serviços podem ser executados individualmente ou como um todo usando Docker. As instruções para configurar o Docker estão na seção de instalação do Docker.

## Testes 
Os testes automáticos podem ser executados usando o comando: `./mvnw test`. Certifique-se de que todos os testes passem antes de fazer o push para o repositório principal.

## Solução de Problemas 
Para resolver problemas comuns, consulte a lista de erros conhecidos e possíveis soluções na pasta `docs` do repositório.

## Configuração de Desenvolvimento 
Para configurar o ambiente de desenvolvimento, instale as dependências necessárias e configure IDE de acordo com as recomendações do projeto nos arquivos de configuração do projeto.

## Diretrizes para Contribuições 
Contribuições são bem-vindas! Para contribuir, crie uma branch a partir da branch `main`, faça suas alterações e envie uma Pull Request.

## Referências 
- [Spring Boot Documentation](https://spring.io/projects/spring-boot) 
- [Microservices Patterns](https://microservices.io) 

Enjoy coding!