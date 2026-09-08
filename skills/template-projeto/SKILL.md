---
name: template-projeto
description: "Aplica ou cria um template reaproveitável de ponta a ponta (estrutura de código + tema visual/UI) para um novo projeto, calibrado pelo porte. Use entre spec-driven e implementacao-guiada, ao iniciar a implementação de um projeto novo."
---

# Template de Projeto

Garante que cada novo projeto comece de um ponto de partida conhecido — estrutura de pastas/convenções de código e uma identidade visual/UI mínima — em vez de reinventar isso do zero (ou de um jeito diferente) toda vez.

## Como conduzir

1. **Verifique se já existe um template aplicável.** Confira `memoria/template.md` (via `memoria-projeto`) de projetos anteriores, ou pergunte ao usuário se ele já tem um template/boilerplate que usa. Um template vale para o porte que foi desenhado (`memoria/porte.md`) — não force um template de projeto grande em um projeto pequeno, nem o contrário.
2. **Se não existir template ainda**, pergunte concretamente, nunca "qual stack você usa" solto: qual linguagem/framework de backend? O projeto tem interface visual? Se sim, qual framework/biblioteca de UI (ou CSS puro)? Existe alguma identidade visual já definida (cores, tipografia), ou criamos uma mínima agora?
3. **Construa o template mínimo necessário para o porte atual** (leia `memoria/porte.md`):
   - Estrutura de pastas e convenções (onde fica cada camada, nomeação).
   - Configs base (lint, formatação, scripts de start/test) — sem inventar ferramentas que o usuário não pediu.
   - Um tema/kit visual mínimo (paleta, tipografia, componentes básicos) se o projeto tiver interface — para garantir consistência visual desde a primeira tela.
4. **Registre o template em `memoria/template.md`** (via `memoria-projeto`): o que ele contém e onde vive, para ser reaproveitado no próximo projeto do mesmo porte.
5. **Aplique o template ao projeto atual** antes de `implementacao-guiada` começar a escrever features.
6. Se um template já existente não cobrir uma necessidade nova do projeto atual, **evolua o template** (não crie uma solução paralela) e registre a mudança.

## Saída

O projeto com a estrutura/tema aplicados, e `memoria/template.md` atualizado com o que foi usado ou criado — para reaproveitar no próximo projeto.