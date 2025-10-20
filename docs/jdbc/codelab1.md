---
title: JDBC - CODELAB 1
---


---

## Codelab: Praticando JDBC

## Objetivo

Aprender a conectar uma aplicação Java a um banco de dados e executar operações básicas de CRUD (Create, Read, Update, Delete).

---

### Passo 1 — Configuração do Ambiente

1. Instale o **MySQL** ou use o **HSQLDB** (modo memória).
2. Adicione o driver JDBC ao projeto (arquivo `.jar`):
   - `mysql-connector-j-8.x.jar`

#### Alternativa: Usando HSQLDB (Banco em Memória)

Para evitar a instalação de um SGBD, podemos usar o **HSQLDB** — um banco leve, 100% Java, que roda em memória.

##### Dependência Maven

Adicione ao seu `pom.xml`:

```xml
<dependencies>
  <dependency>
    <groupId>org.hsqldb</groupId>
    <artifactId>hsqldb</artifactId>
    <version>2.7.4</version>
    <scope>runtime</scope>
  </dependency>
</dependencies>

---

### Passo 2 — Criar a Tabela

```sql
CREATE TABLE aluno (
  id INT PRIMARY KEY,
  nome VARCHAR(100),
  matricula VARCHAR(20)
);
```

### Passo 3 — Estabelecer Conexão

```java
Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/escola","root", "senha");
System.out.println("Conectado!");
```

### Passo 4 — Inserir Registros

```java
PreparedStatement ps = con.prepareStatement("INSERT INTO aluno VALUES (?, ?, ?)");
ps.setInt(1, 1);
ps.setString(2, "Bruno");
ps.setString(3, "2025001");
ps.executeUpdate();
```

### Passo 5 — Consultar Registros

```java
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT * FROM aluno");
while (rs.next()) {
  System.out.printf("%d - %s (%s)%n",
    rs.getInt("id"), rs.getString("nome"), rs.getString("matricula"));
}
```

### Passo 6 — Atualizar e Excluir

```java
stmt.executeUpdate("UPDATE aluno SET nome='João' WHERE id=1");
stmt.executeUpdate("DELETE FROM aluno WHERE id=1");
```

