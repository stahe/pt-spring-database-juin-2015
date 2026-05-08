# Trabalhar com uma base de dados relacional utilizando o ecossistema Spring (junho de 2015)

O objetivo deste projeto é estudar e comparar diferentes arquiteturas de acesso a dados numa aplicação Java baseada no ecossistema **Spring**, nomeadamente **Spring JDBC** e **Spring JPA**, quando aplicadas a uma base de dados relacional.

Os materiais teóricos e didáticos relacionados estão disponíveis aqui:  
👉 https://stahe.github.io/pt-spring-database-juin-2015/

---

## Objetivos do projeto

- Compreender uma **arquitetura de aplicação em camadas**
- Comparar duas abordagens de acesso aos dados:
  - JDBC «clássico»
  - JPA (Java Persistence API)
- Medir e comparar o **desempenho** de ambas as soluções
- Analisar os desafios da **portabilidade entre SGBD**

---

## Arquitetura geral

A aplicação baseia-se numa arquitetura em camadas, onde o fluxo de execução decorre da esquerda para a direita:
![](https://stahe.github.io/spring-database-juin-2015/images/10000000000007080000017A09403716.png)


### Função das camadas

#### Camada de interface do utilizador (UI)
- Ponto de entrada da aplicação
- Recebe as ações do utilizador
- Apresenta os resultados

#### Camada de negócio (Business Layer)
- Implementa **regras de negócio**
- Processa dados provenientes de:
  - a base de dados (através do DAO)
  - o utilizador (através da interface do utilizador)
- Pode devolver ou persistir resultados

#### Camada DAO (objeto de acesso a dados)
- Expõe uma **interface de acesso a dados de negócio**
- Oculta os detalhes técnicos do acesso à base de dados
- Depende da tecnologia utilizada (JDBC ou JPA)

#### Camada JDBC
- Interface padrão para aceder a bases de dados relacionais
- Independente do SGBD (através de controladores JDBC)
- Permite um bom desempenho, mas uma portabilidade limitada na prática

---

## Evolução para JPA

Desde meados da década de 2000, a arquitetura pode evoluir da seguinte forma:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

### Características específicas do JPA

- A camada **JPA** gera consultas SQL
- A camada DAO:
  - já não contém SQL
  - manipula objetos persistentes
- Vantagens:
  - Melhor portabilidade entre SGBDs
  - Abstração do SQL proprietário
- Desvantagens:
  - Desempenho geralmente inferior ao do JDBC

O JPA formaliza conceitos introduzidos anteriormente por frameworks como o **Hibernate**.

---

## Comparação entre JDBC e JPA

O projeto implementa **duas implementações DAO distintas**:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006E10000016947159BE8.png)


### Restrições comuns

- `DAO1` e `DAO2` implementam a **mesma interface `IDAO`**
- Os testes unitários são **idênticos** para ambas as implementações
- Objetivo: comparar a **funcionalidade** e o **desempenho**

---

## Testes e desempenho

- Os testes são realizados utilizando **JUnit**
- É utilizada uma única classe de teste (`JUnitTestsDao`)
- Os resultados permitem-nos:
  - verificar a conformidade funcional
  - comparar os tempos de execução do JDBC em relação ao JPA

---

## Portabilidade do SGBD

Embora o JDBC tenha como objetivo a máxima portabilidade:
- o SQL proprietário;
- as estratégias de geração de chaves primárias;
- as palavras reservadas específicas;

limitam essa portabilidade na prática.

Neste projeto, as arquiteturas JDBC e JPA foram portadas para **seis SGBDs diferentes**, o que exigiu configurações específicas para cada SGBD.

---

## Conclusão

Este projeto ilustra:
- as compensações entre **desempenho** e **abstração**;
- as decisões arquitetónicas relacionadas com o acesso aos dados;
- a contribuição do Spring para a estruturação e a testabilidade das aplicações;

Serve como recurso educativo para adquirir uma compreensão prática do JDBC, do JPA e das suas utilizações comparativas dentro de uma arquitetura Spring.

Serge Tahé, junho de 2015
---
