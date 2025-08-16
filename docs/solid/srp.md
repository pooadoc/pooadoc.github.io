---
title: Single Responsibility Principle
---

**Princípio da Responsabilidade Única (SRP)**

* "Uma classe deve ter somente uma razão para mudar" - Martin, Robert C.

* Dificuldade de compreensão, reuso e responsabilidades entrelaçadas são problemas.
* Alto acoplamento: classe com número excessivo de dependências.

### Exemplo (Antes)

```java
public class Pedido {
    public void adicionarProduto(Produto produto, int quantidade) { }
    public decimal calcularTotal() { }
    public void gerarPlanilhaExcel() { }
}
