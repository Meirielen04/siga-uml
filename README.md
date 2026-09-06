# SIGA —  UML Aplicada a Padrões de Projeto
**Técnicas de Programação II (TP2) · Aula 4** — CST em Desenvolvimento de Software Multiplataforma · Fatec de Porto Ferreira

## 1. Diagrama de Classes do Domínio

```mermaid
classDiagram
    direction TB

    %% Entidades Principais
    class Pessoa {
        #String nome
        #String registro
        #boolean ativo
        +Pessoa(String nome, String registro, boolean ativo)
        +getNome() String
        +setNome(String nome) void
        +getRegistro() String
        +setRegistro(String registro) void
        +getAtivo() boolean
        +setAtivo(boolean ativo) void
        +apresentar() String
    }

    class Aluno {
        -double media
        +Aluno(String nome, String registro, boolean ativo, double media)
        +getMedia() double
        +setMedia(double media) void
        +apresentar() String
    }

    class Professor {
        +Professor(String nome, String registro, boolean ativo)
        +apresentar() String
    }

    class Turma {
        -String codigo
        -List~Aluno~ alunos
        +adicionar(Aluno aluno) void
    }

    class Matricula {
        -Aluno aluno
        -double valorBase
        -Desconto desconto
        +Matricula(Aluno aluno, double valorBase, Desconto desconto)
        +calcularMensalidade() double
        +getValorBase() double
        +setValorBase(double valorBase) void
        +getDesconto() Desconto
        +setDesconto(Desconto desconto) void
        +getAluno() Aluno
    }

    %% Interface e Estratégias de Desconto
    class Desconto {
        <<interface>>
        +calcular(double valorBase) double
    }

    class DescontoBolsista {
        +calcular(double valorBase) double
    }

    class DescontoConvenio {
        +calcular(double valorBase) double
    }

    class DescontoFuncionario {
        +calcular(double valorBase) double
    }

    class SemDesconto {
        +calcular(double valorBase) double
    }


    %% Relacionamentos
    %% Herança / Generalização
    Pessoa <|-- Aluno : herda de
    Pessoa <|-- Professor : herda de

    %% Agregação e Associação do Domínio Acadêmico
    Turma "1" o-- "1..*" Aluno : agrega
    Matricula "*" --> "1" Aluno : pertence a
    Matricula "1" --> "1" Desconto : aplica

    %% Realizações da Interface Desconto
    Desconto <|.. DescontoBolsista : realiza
    Desconto <|.. DescontoConvenio : realiza
    Desconto <|.. DescontoFuncionario : realiza
    Desconto <|.. SemDesconto : realiza
```
## 2. Diagrama de Sequência: Cálculo da Mensalidade

```mermaid
sequenceDiagram
    autonumber
    actor Aluno
    participant Matricula
    participant Desconto

    Cliente ->> Matricula: calcularMensalidade()
    activate Matricula
    Matricula ->> Desconto: calcular(valorBase)
    activate Desconto
    Desconto -->> Matricula: valorComDesconto
    deactivate Desconto
    Matricula -->> Cliente: valorFinal
    deactivate Matricula
```
