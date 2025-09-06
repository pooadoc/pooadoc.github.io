---
title: Adapter
---

> **Definição (GoF):** “Converter a interface de uma classe em outra interface esperada pelos clientes. **Adapter** permite a comunicação entre classes que não poderiam trabalhar juntas devido à incompatibilidade de suas interfaces.”


## Problema
- O **cliente** espera uma **interface-alvo** (Target), mas a implementação disponível expõe uma interface **incompatível** (Adaptee).

```mermaid
  classDiagram
  direction TD
  class Cliente {
    - Alvo alvo
    +Cliente(Alvo a)
    +executar()
  }
  Cliente --> Alvo : usa 
  class Alvo {
    <<interface>>
    +metodo()
  } 
  class CodigoExistente {
    +metodoUtil()
  }
```

- Como **reusar** o código existente (legado/terceiros) **sem alterar** seu contrato, nem quebrar o cliente?

## Solução (visões GoF)
- **Class Adapter** (herança): o adaptador **implementa** `Target` e **herda** de `Adaptee` (em Java, viável quando `Target` é **interface**).

- **Object Adapter** (composição): o adaptador **implementa** `Target` e **compõe** um `Adaptee`, **delegando** chamadas (opção mais flexível/testável).


## Class Adapter

```mermaid
  classDiagram
  direction TD
  class Cliente {
    -alvo : Alvo
    +Cliente(Alvo a)
    +executar()
  }
  Cliente --> Alvo : usa 
  class Alvo {
    <<interface>>
    +metodo()
  } 
  class CodigoExistente {
    +metodoUtil()
  }
  class ClasseAdapter {
    +metodo()
  }
  note for ClasseAdapter "metodo(){ this.metodoUtil()}"
  ClasseAdapter ..|> Alvo : implementa
  CodigoExistente <|--  ClasseAdapter : herda
```

## Object Adapter

```mermaid
  classDiagram
  direction TD
  class Cliente {
    -alvo : Alvo
    +Cliente(Alvo a)
    +executar()
  }
  Cliente --> Alvo : usa 
  class Alvo {
    <<interface>>
    +metodo()
  } 
  class CodigoExistente {
    +metodoUtil()
  }
  class ObjectAdapter {
    -codigoExistente : CodigoExistente
    +metodo()
  }
  note for ObjectAdapter "metodo(){ this.codigoExistente.metodoUtil()}"
  ObjectAdapter ..|> Alvo : implementa
  CodigoExistente --*  ObjectAdapter : tem
```

---

## Exemplo 1: Adapter Problema

```mermaid
  classDiagram
  direction TD

  namespace myApp{
  class CadastroController {
    -servicoCep : ServicoCep
    +Cliente(ServicoCep servicoCep)
  }

  class ServicoCep {
    <<interface>>
    +obterEndereco(String cep): Endereco
  } 
  class Endereco {
    <<interface>>
  } 
  }

  CadastroController --> ServicoCep : usa 
  CadastroController --> Endereco : usa 

  namespace ViaCep{
  class ViaCepService {
    +lookup(String cep): EnderecoViaCep
  }

  class EnderecoViaCep {
  }
   
  }
  ViaCepService --> EnderecoViaCep
```



## Solução

```mermaid
  classDiagram
  direction LR

  namespace myApp{
  class CadastroController {
    -servicoCep : ServicoCep
    +Cliente(ServicoCep servicoCep)
  }

  class ServicoCep {
    <<interface>>
    +obterEndereco(String cep): Endereco
  } 
  class Endereco {
    <<interface>>
  } 

 class CepServiceAdapter {
    -viaCepService : ViaCepService
    +obterEndereco(String cep) Endereco
  }
  class EnderecoAdapter{
    -enderecoViaCep : EnderecoViaCep
  }
}

  note for CepServiceAdapter "obterEndereco(cep){ this.lookup(cep)()}"
  CepServiceAdapter ..|> ServicoCep : implementa
  ViaCepService  <| -- CepServiceAdapter : herda
  CepServiceAdapter --> Endereco

  EnderecoAdapter ..|> Endereco : implementa
  EnderecoViaCep  --* EnderecoAdapter : tem


  CadastroController --> ServicoCep : usa 
  CadastroController --> Endereco : usa 

  namespace ViaCep{
  class ViaCepService {
    +lookup(String cep): EnderecoViaCep
  }

  class EnderecoViaCep
   
   
  }
  ViaCepService --> EnderecoViaCep

```