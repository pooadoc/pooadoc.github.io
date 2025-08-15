# Apache Tomcat


1. Conceitos 

    1.1 O que é TOMCAT?
    Tomcat é um servidor de aplicações web Java (open-source, da Apache) que implementa as especificações Jakarta Servlet, JSP, EL e WebSocket. Em outras palavras, ele é o “motor” que executa aplicações web Java empacotadas como WAR.



    1.2 Versões e suporte de JDK 
    - Tomcat 10.1.x/10.1.y: requer Java 11+ (recomendável Java 17/21).
    - Tomcat 11.x: voltado ao Jakarta EE 11; requer Java 17+ (preferencialmente 21).

    Distribuições:

    - Core (zip/tar.gz): pacote “puro” do Tomcat.

    - Pacotes específicos com serviço Windows e etc.

    1.3 Baixar e descompactar o Core
    - Windows: baixe o .zip
    - Linux/macOS: baixe o .tar.gz

    Descompacte em um caminho sem espaços:
    
    Exemplos:

    Windows: 
    
    C:\Dev\tomcat\apache-tomcat-10.1.x

    Linux/macOS: 
    
    /opt/tomcat/apache-tomcat-10.1.x 

    1.4 Executar o Tomcat
    
    Windows (PowerShell/CMD):

    ```bat
    cd C:\caminho\tomcat\bin
    startup.bat
    ```
    Linux/macOS:

    ```bash
    cd /opt/caminho/tomcat/bin
    ./startup.sh
    ```

    Abra no navegador: http://localhost:8080/

    Conteudo da pagina Inicial:

    Home do Tomcat com links para documentação, Status, e Manager/Host Manager (estes exigem configuração de usuário no conf/tomcat-users.xml).

    Para parar:

    Windows: ```shutdown.bat```

    Linux/macOS: ```./shutdown.sh```

    Estrutura básica do Tomcat:

        bin/ – scripts de inicialização/parada (startup/shutdown, catalina)

        conf/ – configurações (ex.: server.xml, web.xml, tomcat-users.xml)

        lib/ – bibliotecas do servidor

        logs/ – arquivos de log (útil para depuração)

        webapps/ – onde você implanta suas aplicações (.war ou pasta expandida)

        work/ – cache/artefatos gerados em tempo de execução

        temp/ – arquivos temporários





