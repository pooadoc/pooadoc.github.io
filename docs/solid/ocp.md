---
title: Open/Closed Principle
---


!!! note Princípio do Aberto/Fechado (OCP)
"Entidades de software devem ser abertas para extensão mas fechadas para modificação." - Martin, Robert C.

Estender o comportamento com código novo, sem alterar o existente.


O código apresentado a seguir  viola o Princípio do Aberto/Fechado (OCP) porque, para adicionar novos tipos de arquivo ou novos formatos de conversão, é necessário modificar as classes existentes, especialmente GeradorDeArquivos e Arquivo.



```java
//Arquivo.java
public class Arquivo {
    private String tipo;
    private String conteudo;

    public String getTipo(){
        return this.tipo;
    }

    public File convertToDocX(){
        //Codigo para converter para DOCX    
    }

    public File convertToPDF(){
        //Codigo para converter para PDF    
    }

 }

//GeradorDeArquivos.java
public class GeradorDeArquivos {
   public void gerarArquivos(List<Arquivo> arquivos) {
      for(Arquivo arquivo : arquivos) {
        File file;
        if ("DOCX".equals(arquivo.getTipo()))
            file = arquivo.convertToDocX();
        else if ("PDF".equals(arquivo.getTipo()))
            file = arquivo.convertToPDF();
        file.save();
      }
   }
}
```

Explicação do código

- Classe Arquivo

    Possui métodos para converter o arquivo para DOCX e PDF. O tipo do arquivo é definido por uma string.
- Classe GeradorDeArquivos

    Percorre uma lista de arquivos e, dependendo do tipo (getTipo()), chama o método de conversão correspondente. O tipo é verificado com if ("DOCX".equals(arquivo.getTipo())) e else if ("DOCX".equals(arquivo.getTipo())) (há um erro: ambos verificam "DOCX", deveria ser "PDF" no segundo caso).
- Para suportar um novo tipo de arquivo (ex: TXT, HTML), você teria que modificar a classe 
- Arquivo para adicionar novos métodos e também alterar o método gerarArquivos em GeradorDeArquivos para incluir novos if/else.
- Isso significa que o código não está fechado para modificação: toda vez que um novo formato é necessário, o código existente precisa ser alterado.



**Solução**

O correto seria usar abstração (interfaces ou herança), permitindo adicionar novos tipos sem modificar as classes existentes.

criar uma Abstração  Arquivo e implementar para cada tipo uma Classe usando polimorfismo.

Assim, o código fica aberto para extensão (novos tipos de arquivo) e fechado para modificação, seguindo o OCP.


```java
//Arquivo.java
public abstract class Arquivo {
    
    private String conteudo;

    public abstract File convert();
 
}

public class DOCX extends Arquivo {
    
    public abstract File convert(){
    //Codigo para converter para DOCX    
    }
 
}

public class PDF extends Arquivo {
    
    public abstract File convert(){
    //Codigo para converter para PDF    
    }
 
}

public class TXT extends Arquivo {
    
    public abstract File convert(){
    //Codigo para converter para PDF    
    }
 
}

//GeradorDeArquivos.java
public class GeradorDeArquivos {
   public void gerarArquivos(List<Arquivo> arquivos) {
      for(Arquivo arquivo : arquivos) {
        File file = arquivo.convert();
        file.save();
      }
   }
}
```