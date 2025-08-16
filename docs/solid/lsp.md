---
title: Liskov Substitution Principle
---


Princípio de Substituição de Liskov (LSP)

"Se para cada objeto o1 do tipo S há um objeto o2 do tipo T... o comportamento de P é inalterado quando o1 é substituído por o2 então S é um subtipo de T" - Barbara Liskov.

"Classes derivadas devem poder ser substitutas de suas classes base" - Martin, Robert C.

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



A violação do Princípio de Substituição de Liskov (LSP) ocorre porque a classe Diretor, que herda de Colaborador, não pode ser substituída por sua classe base (Colaborador) sem alterar o comportamento esperado do programa.

A classe base Colaborador e a classe Coordenador (que também herda de Colaborador) retornam um Integer válido para o método cargaHoraria. No entanto, a classe Diretor retorna null para o mesmo método. Se o código que chama cargaHoraria espera sempre receber um Integer válido (como a classe base sugere), a substituição de um objeto Colaborador ou Coordenador por um objeto Diretor causará um erro (por exemplo, um NullPointerException) quando tentar usar o valor retornado. Isso demonstra que Diretor não é um subtipo válido de `Colaborador de acordo com o LSP, pois altera o comportamento esperado.


**Solução**

Possível solução:

Para resolver essa violação do LSP, a classe Diretor deve implementar o método cargaHoraria de forma a retornar um Integer válido, mesmo que seja zero ou outro valor que indique que não há carga horária aplicável para um diretor no contexto em questão.
