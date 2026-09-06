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

    %% Relacionamentos
    %% Herança / Generalização
    Pessoa <|-- Aluno : herda de
    Pessoa <|-- Professor : herda de
```
