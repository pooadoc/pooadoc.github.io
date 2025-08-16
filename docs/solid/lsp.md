---
title: Liskov Substitution Principle
---


Princípio de Substituição de Liskov (LSP)

"Se para cada objeto o1 do tipo S há um objeto o2 do tipo T... o comportamento de P é inalterado quando o1 é substituído por o2 então S é um subtipo de T" - Barbara Liskov.

"Classes derivadas devem poder ser substitutas de suas classes base" - Martin, Robert C.

Exemplos

Exemplo 1:

```java
public class A {
    public String getNome(){ return "Meu Nome é A"; }
}

public class B extends A {
    public String getNome(){ return "Meu Nome é B"; }
}

public class Console {
    public static void imprimeNome(A a){
        System.out.println(a.getNome());
    }
    public static void main(){
        imprimeNome(new A());
        imprimeNome(new B());
    }
}
```

Exemplo 2:

```java

public class Colaborador {
    public Integer cargaHoraria(int mes){ 
        //calcula a carga horária para o mes
        return cargahoraria;
    }
}
 
public class Coordenador extends Colaborador {
    public Integer cargaHoraria(int mes){ 
        //calcula a carga horária para o mes
        return cargahoraria;
    }   
}
 
public class Diretor extends Colaborador {
    public Integer cargaHoraria(int mes){ 
        //calcula a carga horária para o mes
        return null;
    }
}
```

A violação do Princípio de Substituição de Liskov (LSP) ocorre porque a classe Diretor, que herda de Colaborador, não pode ser substituída por sua classe base (Colaborador) sem alterar o comportamento esperado do programa.

A classe base Colaborador e a classe Coordenador (que também herda de Colaborador) retornam um Integer válido para o método cargaHoraria. No entanto, a classe Diretor retorna null para o mesmo método. Se o código que chama cargaHoraria espera sempre receber um Integer válido (como a classe base sugere), a substituição de um objeto Colaborador ou Coordenador por um objeto Diretor causará um erro (por exemplo, um NullPointerException) quando tentar usar o valor retornado. Isso demonstra que Diretor não é um subtipo válido de `Colaborador de acordo com o LSP, pois altera o comportamento esperado.

**Solução**

Para resolver essa violação do LSP, a classe Diretor deve implementar o método cargaHoraria de forma a retornar um Integer válido, mesmo que seja zero ou outro valor que indique que não há carga horária aplicável para um diretor no contexto em questão.

```java
public class Diretor extends Colaborador {
    public Integer cargaHoraria(int mes){
        // Implementação que retorna um Integer válido, por exemplo, 0
        return 0;
    }
}
```

Dessa forma, a classe Diretor pode ser substituída por Colaborador sem quebrar o código cliente que espera um Integer válido, respeitando o Princípio de Substituição de Liskov.


Exemplo 3:

Sistema de processamento de pagamentos que lida com diferentes tipos de cartões. Temos uma classe base CartaoCredito e classes derivadas como
CartaoCreditoMaster e CartaoPrePago.

O sistema possui uma função para processar um pagamento, que espera um objeto do tipo CartaoCredito

```java
public class CartaoCredito {
    public void pagar(double valor) {
        System.out.println("Pagamento de R$" + valor + " com cartão de crédito.");
        // Lógica para processar pagamento com cartão de crédito
    }

    public double getLimiteCredito() {
        return 1000.0; // Exemplo de limite padrão
    }
}

public class CartaoCreditoMaster extends CartaoCredito {
    @Override
    public void pagar(double valor) {
        System.out.println("Pagamento de R$" + valor + " com MasterCard.");
        // Lógica específica para MasterCard
    }

    @Override
    public double getLimiteCredito() {
        return 5000.0; // Limite maior para MasterCard
    }
}

public class CartaoPrePago extends CartaoCredito {
    @Override
    public void pagar(double valor) {
        if (valor > 0) { // Um cartão pré-pago não tem limite, mas saldo
            System.out.println("Pagamento de R$" + valor + " com cartão pré-pago. Saldo atualizado.");
            // Lógica para deduzir do saldo do cartão pré-pago
        } else {
            // Um cartão pré-pago não pode ser usado para obter limite de crédito
            throw new UnsupportedOperationException("Operação 'pagar' com valor zero não é suportada para Cartão Pré-Pago.");
        }
    }

    @Override
    public double getLimiteCredito() {
        // Um cartão pré-pago não possui limite de crédito, possui saldo.
        // Retornar 0.0 pode ser enganoso se o cliente espera um limite.
        // Lançar uma exceção é uma violação do LSP.
        throw new UnsupportedOperationException("Cartão Pré-Pago não possui limite de crédito.");
    }
}

public class ProcessadorPagamento {
    public void processar(CartaoCredito cartao, double valor) {
        System.out.println("Verificando limite antes de pagar...");
        // O código espera que qualquer CartaoCredito forneça um limite válido
        if (cartao.getLimiteCredito() >= valor) {
            cartao.pagar(valor);
        } else {
            System.out.println("Crédito insuficiente.");
        }
    }

    public static void main(String[] args) {
        ProcessadorPagamento processador = new ProcessadorPagamento();

        CartaoCreditoMaster master = new CartaoCreditoMaster();
        processador.processar(master, 100.0); // Funciona

        CartaoPrePago prePago = new CartaoPrePago();
        // Isso violará o LSP, pois getLimiteCredito() lançará uma exceção
        processador.processar(prePago, 50.0); 
    }
}
```

A violação do LSP ocorre na classe ```CartaoPrePago```. O método ```getLimiteCredito()```  na classe base ```CartaoCredito``` e em ```CartaoCreditoMaster``` retorna um valor numérico que representa um limite de crédito. No entanto, em ```CartaoPrePago``` , o mesmo método lança uma ```UnsupportedOperationException```.

Quando o ```ProcessadorPagamento``` tenta usar um objeto ```CartaoPrePago```  como se fosse um ```CartaoCredito``` (que ele é, de acordo com a herança), ele espera que ```getLimiteCredito()``` retorne um valor. Ao invés disso, o programa falha com uma exceção em tempo de execução, alterando drasticamente o comportamento esperado e quebrando a premissa de que um subtipo pode ser substituído por seu tipo base sem problemas. Um cartão pré-pago não tem "limite de crédito" no sentido tradicional; ele tem um "saldo".

**Solução**

A solução envolve garantir que os subtipos não alterem o comportamento esperado da classe base de forma que o código cliente não possa prever. 

Isso pode ser feito através de:

* Refatoração da Hierarquia: Criar uma hierarquia mais adequada que reflita as diferentes capacidades.
* Uso de Interfaces: Definir contratos específicos para as operações que cada tipo de cartão realmente suporta.
* Retorno de Valores Padronizados ou Opção: Evitar lançar exceções onde a classe base espera um valor, retornando um valor significativo (ex: 0 para "sem limite") ou usando um tipo opcional (como ```Optional<Double>``` em Java 8+) para indicar a ausência de um limite.

```java
// Interface para cartões que podem ser pagos
public interface ProcessavelPorPagamento {
    void pagar(double valor);
}

// Interface para cartões que possuem limite de crédito
public interface PossuiLimiteCredito {
    double getLimiteCredito();
}

public class CartaoCredito implements ProcessavelPorPagamento, PossuiLimiteCredito {
    @Override
    public void pagar(double valor) {
        System.out.println("Pagamento de R$" + valor + " com cartão de crédito genérico.");
    }

    @Override
    public double getLimiteCredito() {
        return 1000.0;
    }
}

public class CartaoCreditoMaster extends CartaoCredito { // Ainda herda de CartaoCredito
    @Override
    public void pagar(double valor) {
        System.out.println("Pagamento de R$" + valor + " com MasterCard.");
    }

    @Override
    public double getLimiteCredito() {
        return 5000.0;
    }
}

public class CartaoPrePago implements ProcessavelPorPagamento { // Não implementa PossuiLimiteCredito
    private double saldo;

    public CartaoPrePago(double saldoInicial) {
        this.saldo = saldoInicial;
    }

    @Override
    public void pagar(double double valor) {
        if (valor > 0 && this.saldo >= valor) {
            this.saldo -= valor;
            System.out.println("Pagamento de R$" + valor + " com cartão pré-pago. Saldo restante: R$" + this.saldo);
        } else if (valor <= 0) {
            System.out.println("Valor inválido para pagamento.");
        } else {
            System.out.println("Saldo insuficiente no cartão pré-pago.");
        }
    }

    public double getSaldo() { // Método específico para pré-pago
        return saldo;
    }
}

public class ProcessadorPagamentoRefatorado {
    // Agora o processador é mais específico sobre o que ele espera
    public void processar(ProcessavelPor Pagamento cartao, double valor) {
        // Se o cartão tem limite de crédito, podemos verificar
        if (cartao instanceof PossuiLimiteCredito) {
            PossuiLimiteCredito cartaoComLimite = (PossuiLimiteCredito) cartao;
            if (cartaoComLimite.getLimiteCredito() >= valor) {
                cartao.pagar(valor);
            } else {
                System.out.println("Crédito insuficiente.");
            }
        } else {
            // Para outros tipos de cartões (como pré-pago), apenas tenta pagar
            cartao.pagar(valor);
        }
    }

    public static void main(String[] args) {
        ProcessadorPagamentoRefatorado processador = new ProcessadorPagamentoRefatorado();

        CartaoCreditoMaster master = new CartaoCreditoMaster();
        processador.processar(master, 100.0);

        CartaoPrePago prePago = new CartaoPrePago(200.0);
        processador.processar(prePago, 50.0);
        // Completando a chamada que faltava
        processador.processar(prePago, 180.0); // Tentando um pagamento maior que o saldo restante
    }
}
```
