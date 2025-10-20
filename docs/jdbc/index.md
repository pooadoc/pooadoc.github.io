---
title: JDBC
---

## Fundamentos de JDBC (Java DataBase Connectivity)

**JDBC (Java DataBase Connectivity)** é uma interface padrão em Java para acesso a bancos de dados relacionais.  
Ela permite que aplicações Java executem comandos **SQL** e manipulem os resultados, independentemente do SGBD.

- Pacote principal: `java.sql`
- Inspirada no modelo ODBC
- Compatível com qualquer SGBD que possua **driver JDBC**


## Tipos de Drivers JDBC

| Tipo | Descrição | Características |
|------|------------|----------------|
| **1** | Ponte ODBC-JDBC | Requer software cliente |
| **2** | Código nativo (C/C++) | Depende de API local |
| **3** | Middleware (100% Java no cliente) | Traduz comandos via rede |
| **4** | 100% Java puro | Comunicação direta com o SGBD via sockets |

## URL JDBC

Formato geral:

```bash
jdbc:<subprotocolo>:<dsn>
```

**Exemplos:**

```bash
- `jdbc:odbc:anuncios`
- `jdbc:mysql://localhost:3306/clientes`
- `jdbc:oracle:thin:@localhost:1521:exemplo`
```

---

## Classes Principais

### `DriverManager`

- Gerencia os drivers registrados.
- Retorna uma `Connection` para um banco de dados.

```java
Class.forName("com.mysql.cj.jdbc.Driver");
Connection con = DriverManager.getConnection(
  "jdbc:mysql://localhost:3306/escola", "user", "senha");
```

### Connection

Representa a conexão com o banco.

### Statement

Permite enviar instruções SQL ao banco.

### ResultSet 

Cursor para percorrer os resultados retornados por uma query.

**Exemplo:**

```java
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT nome FROM alunos");

while (rs.next()) {
    System.out.println(rs.getString("nome"));
}

rs.close();
stmt.close();
con.close();
```

### Transações

Por padrão, cada comando é executado automaticamente.
Para controlar transações manualmente:

```java
con.setAutoCommit(false);
// executa várias instruções
con.commit(); // confirma
// ou
con.rollback(); // desfaz
```

## PreparedStatement

Permite instruções pré-compiladas com parâmetros:

```java
String sql = "INSERT INTO alunos (id, nome) VALUES (?, ?)";
PreparedStatement ps = con.prepareStatement(sql);
ps.setInt(1, 1);
ps.setString(2, "Bruno");
ps.executeUpdate();
```

## CallableStatement (Stored Procedures)

```java
CallableStatement cs = con.prepareCall("{call atualizaAluno(?)}");
cs.setInt(1, 5);
cs.execute();
```

## Metadados

```java
DatabaseMetaData dbm = con.getMetaData();
System.out.println(dbm.getDatabaseProductName());

ResultSetMetaData meta = rs.getMetaData();
System.out.println(meta.getColumnCount());
```

## Padrões de Projeto implementados:

Bridge

Abstract Factory

Factory Method

Iterator

## Atividade 
- JDBC: [Codlab 1](codelab1.md)
