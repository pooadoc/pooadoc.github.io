---
title: Single Responsibility Principle
---

## Princípio da Responsabilidade Única (SRP)

* "Uma classe deve ter somente uma razão para mudar" - Martin, Robert C.

* Dificuldade de compreensão, reuso e responsabilidades entrelaçadas são problemas.
* Alto acoplamento: classe com número excessivo de dependências.

## Exemplos

### Exemplo 1

A classe Pedido está misturando responsabilidades: ela cuida tanto da lógica do pedido quanto da geração de relatórios. Se a forma de gerar planilhas mudar, ou se for necessário exportar para outro formato, a classe precisará ser alterada por motivos diferentes, violando o SRP.

```java
public class Pedido {
    public void adicionarProduto(Produto produto, int quantidade) { }
    public decimal calcularTotal() { }
    public void gerarPlanilhaExcel() {
        //Codigo para gerar a planilha
     }
}
```

A classe Pedido possui três métodos:

* adicionarProduto: adiciona produtos ao pedido (regra de negócio).
* calcularTotal: calcula o valor total do pedido (regra de negócio).
* gerarPlanilhaExcel: gera uma planilha Excel com os dados do pedido (responsabilidade de exportação/relatório).


**Solução**

* A classe Pedido cuida apenas da lógica do pedido.
* A classe Excel é responsável por gerar a planilha.

```java
public class Pedido {
    public void adicionarProduto(Produto produto, int quantidade) { }
    public decimal calcularTotal() { }
}

public class Excel {
        public void gerarPlanilhaExcel(Pedido pedido) { 
            //Codigo para gerar a planilha
        }
}
```


Cada classe tem uma única razão para mudar. Se a exportação para Excel mudar, apenas a classe Excel será alterada. Se a lógica do pedido mudar, apenas a classe Pedido será alterada. Isso facilita manutenção, reuso e evolução do sistema, seguindo o Princípio da Responsabilidade Única.


### Exemplo 2

O SRP diz que uma classe deve ter apenas uma razão para mudar, ou seja, deve ser responsável por apenas uma parte da funcionalidade do sistema.


```java
public class Usuario {
    private String nome;
    private String email;

    public void salvar() {
        // Código para salvar o usuário no banco de dados
    }

    public void enviarEmailBoasVindas() {
        // Código para enviar e-mail de boas-vindas
    }
}
```

* A classe Usuario tem duas responsabilidades: persistência (salvar no banco) e comunicação (enviar e-mail).

* Se a forma de salvar mudar, ou a forma de enviar e-mail mudar, a classe precisa ser alterada por motivos diferentes.

**Solução**

* Cada classe tem uma única responsabilidade.

* Mudanças em persistência ou envio de e-mail não afetam a classe Usuario.

```java
public class Usuario {
    private String nome;
    private String email;
    // Apenas dados e regras de negócio do usuário
}

public class UsuarioRepository {
    public void salvar(Usuario usuario) {
        // Código para salvar no banco
    }
}

public class EmailService {
    public void enviarBoasVindas(Usuario usuario) {
        // Código para enviar e-mail
    }
}
```

O código do SRP mostra que misturar responsabilidades em uma classe dificulta manutenção e evolução. Separar cada responsabilidade em sua própria classe facilita mudanças e segue o princípio.
