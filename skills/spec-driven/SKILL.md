---
name: spec-driven
description: "Transforma a ideia e o modelo de domínio numa spec verificável (casos de uso, critérios de aceitação, contratos calibrados pelo porte, pilares de UI/UX obrigatórios), extraindo tudo por perguntas concretas. Use antes de implementar."
---

# Spec-Driven Development

Transforma a ideia e o modelo de domínio numa especificação formal, verificável, que vai guiar a implementação — sem virar burocracia.

## Como conduzir

1. **Verifique primeiro `memoria/brief.md`, `memoria/dominio.md` e `memoria/porte.md`** (skill `memoria-projeto`) — se existirem, use-os como base. Depois, para cada ação identificada no domínio, extraia os casos de uso com perguntas concretas, nunca com uma pergunta aberta sobre "o que a feature precisa fazer": o que acontece quando essa ação dá certo? o que pode dar errado, e o que deve acontecer nesse caso? quem pode fazer essa ação, e quem não pode?
2. **Para cada capacidade/caso de uso**, escreva a partir dessas respostas:
   - Critérios de aceitação no formato Dado/Quando/Então (ou equivalente).
   - Entradas, saídas e casos de erro esperados.
   - **Não-objetivos explícitos** — o que fica de fora, para evitar escopo crescendo sozinho.
3. **Para todo caso de uso com interface**, inclua também critérios de aceitação de UI/UX — não são opcionais quando há tela envolvida:
   - **Consistência visual**: a tela usa o tema/componentes definidos em `template.md` (skill `template-projeto`), não um estilo próprio inventado na hora.
   - **Responsividade**: a tela funciona em pelo menos um tamanho pequeno (mobile) e um grande (desktop).
   - **Usabilidade básica**: estados de carregamento, erro e sucesso são visíveis ao usuário — nenhuma ação fica "muda" sem feedback.
4. **Defina contratos mínimos necessários** (formato de API, assinatura de função, schema de dados), calibrando a formalidade pelo porte (`memoria/porte.md`): em projetos **pequenos**, o suficiente pra implementar e testar, sem documentação formal; em **médios**, contratos mais explícitos e versionados; em **grandes**, contratos tratados como publicados entre serviços/times, com compatibilidade a preservar.
5. **Marque explicitamente pontos sensíveis de segurança** (autenticação, validação de entrada, exposição de dados) dentro da spec — isso alimenta diretamente os checks das skills `implementacao-guiada` e `harness`.
6. Trate a spec como **documento vivo**: se a realidade discordar dela durante a implementação, atualize a spec, não finja que ela é imutável.

## Saída

Um documento de spec com os casos de uso, critérios de aceitação (incluindo UI/UX quando houver tela), contratos e não-objetivos. Grave em `memoria/spec.md` via `memoria-projeto`. Termine perguntando se quer seguir para `template-projeto`, agora que "pronto" e "correto" estão definidos.