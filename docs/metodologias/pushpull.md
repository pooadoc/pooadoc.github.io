---
title: Metodologias Puxadas e Empurradas no Desenvolvimento de Software
--- 

## Entendendo os conceitos, o histórico e exemplos práticos

No desenvolvimento de software, duas lógicas fundamentais orientam como o trabalho flui dentro das equipes: **metodologias empurradas (push)** e **metodologias puxadas (pull)**. Esses conceitos, originados na indutria de manufatura e popularizados pelo Sistema Toyota de Produção, foram adaptados ao contexto de software e influenciaram metodologias modernas como Scrum, Kanban, XP e Lean Software Development.

## 1. O que é uma metodologia “empurrada” (push)?

A abordagem **push** se baseia em **planejar e empurrar trabalho para o time**, independentemente da capacidade real no momento. O fluxo é dirigido por decisões centralizadas e por estimativas prévias.

### Características
- Planejamento antecipado e detalhado.  
- Alocação rígida de tarefas.  
- Escopo definido previamente.  
- Pressupõe previsibilidade de esforço e tempo.  
- Tendência a aumento de *Work in Progress* (WIP).

### Origem histórica
O modelo push deriva:
- da engenharia tradicional (modelo cascata),
- do gerenciamento clássico baseado em cronogramas,
- das linhas de produção da primeira metade do século XX.

### Exemplos de metodologias push
- **Waterfall (Cascata)**  
- **RUP (Rational Unified Process)**  
- **Modelos orientados por cronograma** (Gantt, PERT)

## 2. O que é uma metodologia “puxada” (pull)?

A abordagem **pull** permite que o time **puxe** trabalho conforme sua capacidade real, priorizando fluxo, redução de desperdício e adaptação contínua.

### Características
- Trabalho entra conforme a disponibilidade da equipe.  
- Priorização contínua e orientada a valor.  
- Transparência do fluxo.  
- Redução de multitarefas e sobrecarga.  
- Adaptação constante às mudanças.

### Origem histórica
Inspirada no **Just-in-Time** e no **Lean Manufacturing** (Toyota, 1950–1970), a abordagem pull foi incorporada ao software a partir de 2000, principalmente por:
- **Lean Software Development** (Poppendieck),  
- **Kanban aplicado à TI** (David J. Anderson).

### Exemplos de metodologias pull
- **Kanban** (exemplo mais puro)  
- **Lean Software Development**  
- **Scrum (parcialmente)** — dentro do sprint, o time puxa tarefas do backlog.

## 3. Comparação direta

| Aspecto | Push (Empurrada) | Pull (Puxada) |
|--------|-------------------|----------------|
| Entrada de trabalho | Empurrada via planejamento | Puxada conforme capacidade |
| Controle | Coordenadores/Gestores | Equipe |
| Flexibilidade | Baixa | Alta |
| WIP | Alto | Baixo e limitado |
| Ideal para | Projetos previsíveis | Ambientes incertos e evolutivos |
| Riscos | Sobrecarga, retrabalho | Fluxo lento se a priorização falhar |


## 4. Como aparece em metodologias modernas?

### Scrum
- **Push**: o sprint é planejado e “empurrado” para o time.  
- **Pull**: dentro do sprint, desenvolvedores puxam tarefas do backlog do sprint.

### Kanban
- 100% puxado.  
- Limites de WIP controlam a entrada de trabalho.  
- Fluxo contínuo.

### XP (Extreme Programming)
- Ciclos curtos e feedback rápido.  
- Práticas como refactoring e integração contínua funcionam como sistemas *pull*.

### Lean Software Development
- Baseado totalmente em princípios de fluxo e eliminação de desperdícios.  
- Enfatiza sistemas puxados como parte do desenvolvimento enxuto.


## Impontante

A distinção entre metodologias empurradas e puxadas ajuda a entender como o trabalho deve fluir dentro das equipes.  
- **Push** é útil em contextos previsíveis e com requisitos estáveis.  
- **Pull** se adapta melhor à incerteza, inovação e desenvolvimento iterativo — características presentes na maioria dos projetos modernos.

A escolha, portanto, não é binária; muitas equipes combinam os dois modelos para criar um processo equilibrado que respeite a capacidade da equipe e maximize a entrega de valor.
