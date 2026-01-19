# Crypto API

> **API REST** - Uma API completa para gestão de carteira de criptomoedas demonstrando boas práticas de desenvolvimento Spring Boot.

[![Java](https://img.shields.io/badge/Java-21-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.2.0-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

## Sobre o Projeto

O **Crypto API** é uma API REST desenvolvida em Spring Boot para simular uma carteira de criptomoedas, permitindo realizar todas as operações CRUD (Create, Read, Update e Delete) sobre transações de criptomoedas. Este projeto demonstra boas práticas de desenvolvimento backend, arquitetura limpa e uso de tecnologias modernas do ecossistema Spring.

### Objetivos

- Demonstrar implementação de **API REST** completa com Spring Boot
- Implementar operações CRUD completas sobre transações de criptomoedas
- Aplicar boas práticas de desenvolvimento (validações, tratamento de erros, estrutura modular)
- Servir como **portfólio técnico** demonstrando competências em desenvolvimento backend

## Arquitetura

### Estrutura do Projeto

O projeto segue uma arquitetura em camadas tradicional, organizada por responsabilidades:

```
cryptoapp/
├── controller/          # Camada de apresentação (REST endpoints)
├── entity/             # Entidades JPA (modelo de domínio)
├── repository/         # Camada de acesso a dados (JPA Repository)
├── dto/                # Data Transfer Objects
└── CryptoApplication.java
```

### Camadas

- **Controller**: Expõe endpoints REST para operações sobre criptomoedas
- **Entity**: Modelo de domínio mapeado para o banco de dados
- **Repository**: Abstração de acesso a dados usando JPA
- **DTO**: Objetos de transferência de dados para agregações e consultas

## Stack Tecnológica

### Core
- **Java 21** - Linguagem de programação
- **Spring Boot 3.2.0** - Framework principal
- **Spring Data JPA** - Persistência de dados
- **Spring Web** - Construção de APIs REST

### Banco de Dados
- **H2 Database** - Banco em memória para desenvolvimento (padrão)
- **MySQL** - Banco de dados relacional para produção (configurável)

### Modos de Execução

O projeto foi projetado para rodar **sem necessidade de infraestrutura complexa**, oferecendo dois modos de execução:

- **Desenvolvimento**: H2 em memória para rodar rapidamente sem configuração
- **Produção**: MySQL para ambiente de produção (configuração opcional)

Esta abordagem demonstra flexibilidade: desenvolvimento rápido sem complexidade desnecessária, com opção de usar banco de dados robusto quando necessário.

### Ferramentas
- **Apache Maven** - Gerenciamento de dependências e build
- **H2 Console** - Interface web para visualização do banco de dados durante desenvolvimento

## Estrutura do Projeto

```
Projeto-Crypto-API-Java-Spring-Boot/
├── src/
│   ├── main/
│   │   ├── java/com/aronalvarenga/cryptoapp/
│   │   │   ├── controller/        # REST Controllers
│   │   │   │   └── CoinController.java
│   │   │   ├── entity/            # Entidades JPA
│   │   │   │   └── Coin.java
│   │   │   ├── repository/       # Repositórios JPA
│   │   │   │   └── CoinRepository.java
│   │   │   ├── dto/               # Data Transfer Objects
│   │   │   │   └── CoinTransationDTO.java
│   │   │   └── CryptoApplication.java
│   │   └── resources/
│   │       ├── application.properties
│   │       └── data.sql           # Scripts de inicialização (se houver)
│   └── test/
│       └── java/com/aronalvarenga/cryptoapp/
├── pom.xml
└── README.md
```

## Como Executar

### Pré-requisitos

- **Java 21** ou superior
- **Maven 3.6+** (ou use o wrapper: `./mvnw`)
- **MySQL** (opcional, apenas se quiser usar MySQL ao invés de H2)

### Executando Localmente

1. **Clone o repositório**
   ```bash
   git clone https://github.com/aron-alvarenga/Projeto-Crypto-API-Java-Spring-Boot.git
   cd Projeto-Crypto-API-Java-Spring-Boot
   ```

2. **Configure o banco de dados** (escolha uma opção)

   **Opção A: H2 (recomendado para desenvolvimento rápido)**
   - A aplicação usa H2 por padrão, sem necessidade de configuração adicional
   - Ideal para desenvolvimento e testes rápidos
   - Console H2 disponível em: `http://localhost:8080/h2-console`
   
   **Opção B: MySQL (para produção)**
   - Crie um banco de dados MySQL chamado `cryptodb`
   - Descomente as linhas de configuração MySQL no arquivo `application.properties`
   - Comente ou remova as linhas de configuração H2
   - Configure usuário e senha conforme necessário

3. **Execute a aplicação**
   ```bash
   mvn spring-boot:run
   ```
   ou
   ```bash
   ./mvnw spring-boot:run  # Usando Maven wrapper
   ```

4. **Acesse a aplicação**
   - API Base: `http://localhost:8080`
   - H2 Console: `http://localhost:8080/h2-console` (quando usando H2)
     - JDBC URL: `jdbc:h2:mem:cryptodb`
     - Username: `sa`
     - Password: (deixe em branco)

## Endpoints da API

### Base URL
```
http://localhost:8080/coin
```

### Operações Disponíveis

#### 1. Listar todas as transações agregadas
```http
GET /coin
```

**Resposta:**
```json
[
  {
    "name": "BITCOIN",
    "quantity": 1.5
  },
  {
    "name": "ETHEREUM",
    "quantity": 10.0
  }
]
```

#### 2. Buscar transações por nome da criptomoeda
```http
GET /coin/{name}
```

**Exemplo:**
```http
GET /coin/BITCOIN
```

**Resposta:**
```json
[
  {
    "id": 1,
    "name": "BITCOIN",
    "price": 50000.00,
    "quantity": 1.0,
    "dateTime": "2024-01-15T10:30:00"
  }
]
```

#### 3. Criar nova transação
```http
POST /coin
Content-Type: application/json
```

**Body:**
```json
{
  "name": "BITCOIN",
  "price": 50000.00,
  "quantity": 0.5
}
```

**Resposta:**
```json
{
  "id": 1,
  "name": "BITCOIN",
  "price": 50000.00,
  "quantity": 0.5,
  "dateTime": "2024-01-15T10:30:00"
}
```

#### 4. Atualizar transação existente
```http
PUT /coin
Content-Type: application/json
```

**Body:**
```json
{
  "id": 1,
  "name": "BITCOIN",
  "price": 51000.00,
  "quantity": 0.5
}
```

#### 5. Deletar transação
```http
DELETE /coin/{id}
```

**Exemplo:**
```http
DELETE /coin/1
```

## Modelo de Dados

### Entidade Coin

```java
@Entity
@Table(name = "coin")
public class Coin {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;
    
    private String name;           // Nome da criptomoeda (ex: BITCOIN, ETHEREUM)
    private BigDecimal price;      // Preço unitário da criptomoeda
    private BigDecimal quantity;   // Quantidade da criptomoeda
    private Timestamp dateTime;    // Data e hora da transação
}
```

## Funcionalidades

- [x] CRUD completo de transações de criptomoedas
- [x] Agregação de transações por nome da criptomoeda
- [x] Busca de transações por nome (com LIKE)
- [x] Suporte a H2 (desenvolvimento) e MySQL (produção)
- [x] Console H2 habilitado para visualização de dados
- [x] Validações e tratamento de erros

## Diferenciais Técnicos

### Boas Práticas Implementadas

- **Arquitetura em camadas** clara e organizada
- **Separação de responsabilidades** (Controller, Repository, Entity)
- **Uso de DTOs** para agregações e consultas específicas
- **Configuração flexível** entre H2 e MySQL
- **Tratamento de erros** com códigos HTTP apropriados
- **JPA/Hibernate** para mapeamento objeto-relacional
- **Timestamps automáticos** para rastreamento de transações

## Testes

### Executando Testes

```bash
# Todos os testes
mvn test

# Testes específicos
mvn test -Dtest=CoinControllerTest
```

### Estratégia de Testes (planejado)

- **Testes Unitários**: Lógica de negócio e validações
- **Testes de Integração**: Endpoints REST e persistência
- **Testes de Contrato**: Validação de DTOs e respostas

## Documentação

### Planejado

- [ ] **API Documentation** (Swagger/OpenAPI)
- [ ] **Postman Collection** para testes de API
- [ ] **Diagramas** de arquitetura e fluxo de dados

## Roadmap

### v1.0 - MVP (Atual)
- CRUD completo de transações
- Suporte a H2 e MySQL
- Agregações básicas

### v1.1 - Melhorias
- [ ] Validações de entrada mais robustas
- [ ] Documentação Swagger/OpenAPI
- [ ] Testes unitários e de integração
- [ ] Tratamento de erros padronizado (Problem Details / RFC 7807)

### v2.0 - Expansão
- [ ] Autenticação e autorização (Spring Security)
- [ ] Rate limiting
- [ ] Cache de consultas frequentes
- [ ] Logs estruturados
- [ ] Métricas e observabilidade (Actuator)

### v3.0 - Funcionalidades Avançadas
- [ ] Integração com APIs de cotações em tempo real
- [ ] Cálculo de lucro/prejuízo por transação
- [ ] Relatórios e dashboards
- [ ] Exportação de dados (CSV/Excel)

## Contribuindo

Este é um projeto de portfólio pessoal. Contribuições são bem-vindas! Sinta-se à vontade para abrir issues e pull requests.

## Licença

Este projeto está sob a licença MIT. Veja o arquivo [LICENSE](LICENSE) para mais detalhes.

## Autor

**Aron Alvarenga**

- GitHub: [@aron-alvarenga](https://github.com/aron-alvarenga)
- LinkedIn: [Aron Alvarenga](https://www.linkedin.com/in/aron-alvarenga)

## Agradecimentos

- Spring Framework e comunidade Spring
- Todos os mantenedores das bibliotecas open-source utilizadas

---

**Nota**: Este projeto demonstra uma implementação prática e funcional de uma API REST usando Spring Boot, focando em simplicidade e boas práticas de desenvolvimento. O uso de H2 em desenvolvimento permite execução rápida sem necessidade de configuração de infraestrutura, enquanto a opção de MySQL garante robustez para ambientes de produção.
