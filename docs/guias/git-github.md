---
title: Git, Github e Github Classroom
---

## Objetivo

Apresentar as ferramentas Git, GitHub e GitHub Classroom como suporte às aulas práticas da disciplina **Programação Orientada a Objetos Avançada**. O guia da instalação até a entrega de atividades avaliativas.

---

## 1. Git

### O que é?

- Sistema de **controle de versão distribuído**.
- Permite rastrear mudanças no código, colaborar em equipe e recuperar versões anteriores.

### Instalação

- **Windows/Mac/Linux:** [https://git-scm.com/downloads](https://git-scm.com/downloads)
- Após instalar, configure:

```bash
git config --global user.name "Seu Nome"
git config --global user.email "seuemail@exemplo.com"
```

### Comandos básicos

```bash
git init                # inicia um repositório local
git clone <url>         # clona um repositório remoto
git status              # verifica o status das alterações
git add <arquivo>       # adiciona arquivo à área de stage
git commit -m "mensagem" # registra a alteração
git push                # envia para o GitHub
git pull                # baixa alterações do GitHub
```

---

## 2. GitHub

### O que é?

- Plataforma de hospedagem de repositórios Git.
- Permite colaboração, versionamento e integração com ferramentas como GitHub Actions.

### Passos iniciais (Recomentado)

1. Criar conta ou acessar sua conta : [https://github.com](https://github.com)
2. Adcionar o email da UCSAL como um segundo email da sua conta.

---

## 3. GitHub Classroom

### O que é?

- Ferramenta do GitHub para gerenciar atividades de sala de aula.
- O professor cria **tarefas** e cada aluno recebe um repositório individual já configurado.

### Como funciona para o aluno

1. O professor envia o **link da atividade**.
2. O aluno clica e o GitHub cria um repositório pessoal com a atividade.
3. O aluno clona o repositório para sua máquina:

```bash
git clone https://github.com/pooadoc/atividade-xyz.git
```

4. Faz as alterações localmente.

5. Envia as soluções:

```bash
git add .
git commit -m "Resolução da atividade"
git push origin main
```

---

## 4. Boas práticas

- As atividades avaliativas serão distribuídas via **GitHub Classroom**.
- A correção podem ser automatizada com **GitHub Actions (Autograding)**.
- Critérios:
  - Compilação do código
  - Execução dos testes unitários
  - Estrutura e clareza do código
  - Versionamento adequado (commits pequenos e claros)

---

## 5. Dicas

- Eclipse: Depois de clonar o projeto use o menu **File > Import**.
    1. Digite '''Maven'''.
    2. Selecione Existente Maven Project
    3. Selecione a pasta do projeto (Veja o /src). Clique em proximo.
    4. Verifique se aparece ./pom.xml (selecione). Clique em Finish.


- **Commits pequenos e frequentes**, com mensagens claras:

```bash
git commit -m "Implementa classe Usuario com validação de email"
```

- **Não subir arquivos binários** (ex.: `.class`, `/target`).
