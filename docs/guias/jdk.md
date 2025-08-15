# JDK


1. Conceitos 

    1.1 O que é “JDK” e quais existem?
    O JDK (Java Development Kit) inclui o compilador javac, a JVM e ferramentas de desenvolvimento.

    Distribuições:(Java SE):
    - OpenJDK
    - AWS Corretto
    - Eclipse Temurin (Adoptium)
    - Oracle JDK
    - Microsoft Build of OpenJDK Liberica, Zulu, Red Hat, entre outros

    Todas implementam o padrão Java SE. A diferença está em licenças, suporte e empacotamento.

    Ciclo de lançamento e versões LTS:
    - Uma nova versão a cada 6 meses (março e setembro).
    - Algumas versões são LTS (Long-Term Support), recebendo atualizações por vários anos (ex.: 8, 11, 17, 21).
    - Atuamente as versões LTS são lançadas a cada 2 anos.
    - Para uso em produção, prefira LTS.

2. Instalação

    Escolha do JDK: AWS Corretto (recomendado)

    Por que Corretto?
    - 100% compatível com Java SE
    - Atualizações de segurança e correções
    - Gratuito e multiplataforma

    Download do arquivo: 
    [link](https://docs.aws.amazon.com/corretto/latest/corretto-21-ug/downloads-list.html)
    - Windows: baixe o .zip do Corretto (x64)
    - Linux/macOS: baixe o .tar.gz correspondente à sua CPU (x64/ARM)

    Descompactar o arquivo

    Dê preferencia a caminhos sem espaço:

    Windows: C:\Dev\jdk\corretto-21

    Linux/macOS: /opt/corretto-21 ou ~/dev/corretto-21

    Evite C:\Program Files\... para simplificar JAVA_HOME.


    3. Configurar Variaveis de Ambiente

    PATH

    é a variável de ambiente que lista pastas onde o sistema procura executáveis quando você digita um comando (ex.: java, mvn, git) sem informar o caminho completo.
    
    Como funciona: o shell percorre as pastas do PATH na ordem. Se encontrar java.exe/java, ele executa.
    
    Separador:

    - Windows: ;

    - Linux/macOS: :

    Comandos:

    Exibir o PATH:
    
    - Windows (PowerShell):
    ```bash 
    $env:Path
    ``` 

    Linux/macOS (bash/zsh):
    ```bash
    echo "$PATH"
    ```

    JAVA_HOME

    variável de ambiente que aponta para a pasta raiz do JDK (não é o bin, nem só o JRE).

    Exibir o JAVA_HOME:
    
    - Windows (PowerShell):
    ```bash 
    $env:JAVA_HOME
    ``` 

    Linux/macOS (bash/zsh):
    ```bash
    echo "$JAVA_HOME"
    ```

    Dfinindo o JAVA_HOME

    Windows (PowerShell, sessão atual)
    ```bash
    $env:JAVA_HOME = "C:\caminho\do\jdk"
    ```

    Windows (Painel)

    Pesquise “Variáveis de Ambiente”.

    Em Variáveis do Sistema, crie/edite:

    JAVA_HOME = C:\caminho\do\jdk

    Linux/macOS
    ```bash
    export JAVA_HOME=/opt/caminho/jdk
    ```

    Linux/macOS (permanente)
    ```bash
    echo 'export JAVA_HOME=/opt/caminho/jdk' >> ~/.bashrc
    source ~/.bashrc
    ```

    Boas práticas & armadilhas comuns

    JAVA_HOME deve apontar para o JDK raiz, não para bin e não para um JRE “capado”.

    Evite espaços no caminho do JDK (ex.: prefira C:\Dev\jdk\... a C:\Program Files\...).

    Se houver múltiplas versões de Java, confira qual está no PATH e se bate com o JAVA_HOME.

    Para erros do Tomcat (“JAVA_HOME não definido”): defina JAVA_HOME corretamente e reabra o terminal/serviço.

