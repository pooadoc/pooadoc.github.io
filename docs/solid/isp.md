---
title: Interface Segregation Principle
---

Princípio da Segregação de Interface (ISP)

"É melhor criar interfaces mais específicas ao invés de termos uma única interface genérica." - Martin, Robert C.

```java
public interface Ave {
    public void voar();
    public void comer();
}

public class Aguia implements Ave { /* voar, comer */ }

public class Pinguim implements Ave {
    public void voar(){ /* Não voa! */ }
    public void comer(){ }
}
```

