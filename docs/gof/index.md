---
title: Padrões de Projeto - GoF
---


## Objetivos

- Apresentar os **23 padrões clássicos GoF** (Gang of Four).
- Entender **o problema que solucionam**, a **solução proposta**, diagramas UML e exemplos em Java.
- Refletir sobre **aplicações típicas** e boas práticas em orientação a objetos.
- Explorar também **padrões GRASP** e padrões emergentes como **Injeção de Dependência** e **Aspectos**:contentReference[oaicite:5]{index=5}.

---

## O que é um Padrão?

- **Maneira testada/documentada** de alcançar um objetivo.  
- Padrões existem em diversas áreas da engenharia (arquitetura, urbanismo, software).  
- Em software, **Design Patterns** são soluções para problemas recorrentes na **engenharia de software orientada a objetos**, aplicando classes, métodos e boas práticas:contentReference[oaicite:6]{index=6}.  
- Inspirados no livro *A Pattern Language* de **Christopher Alexander**, que descreve padrões de cidades, casas e prédios.

---

## Importância dos Padrões

- **Aprender com a experiência** de outros desenvolvedores.  
- **Vocabulário comum**: facilita comunicação e documentação.  
- **Reduz complexidade**: permite falar em alto nível de abstração.  
- **Boas práticas em OO**: reutilização, eficiência, alta coesão e baixo acoplamento.  
- **Ajuda na aprendizagem**: padrões tornam sistemas existentes mais fáceis de entender:contentReference[oaicite:7]{index=7}.

---

## Elementos de um Padrão

Todo padrão segue uma estrutura:

- **Nome**: termo que identifica o padrão.
- **Problema**: quando aplicá-lo, em que condições.
- **Solução**: arranjo de classes/objetos que resolve o problema.
- **Consequências**: impactos positivos/negativos, custos, flexibilidade e eficiência:contentReference[oaicite:8]{index=8}.

---

## O Livro GoF

- Publicado em **1994** por **Erich Gamma, Richard Helm, Ralph Johnson e John Vlissides**.  
- Catálogo de **23 padrões de projeto** para OO.  
- Tornou-se um clássico e continua atual.  
- Os autores ficaram conhecidos como **Gang of Four (GoF)**:contentReference[oaicite:9]{index=9}.

---

## Classificação dos Padrões (GoF)

Os padrões são classificados **por propósito** e **por escopo**:

### Tabela (Propósito × Escopo)

| Propósito        | Classe               | Objeto                                                                 |
|------------------|----------------------|------------------------------------------------------------------------|
| **Criação**      | Factory Method       | Abstract Factory, Builder, Prototype, Singleton                        |
| **Estrutura**    | Class Adapter        | Object Adapter, Bridge, Composite, Decorator, Facade, Flyweight, Proxy |
| **Comportamento**| Template Method      | Interpreter, Chain of Responsibility, Command, Iterator, Mediator, Memento, Observer, State, Strategy, Visitor |

Fonte: Gamma et al., *Design Patterns (1994)*:contentReference[oaicite:10]{index=10}.

---

## Organização deste material

- [Factory Method](factory-method.md)
- [Abstract Factory](abstract-factory.md)
- (Outros padrões podem ser adicionados conforme avançarmos no curso.)

---
