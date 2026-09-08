---
name: brainstorming
description: "Explora um projeto ou feature nova antes de decidir o que construir: gera alternativas reais, questiona a ideia inicial e converge numa direção, checando e gravando o resultado em memoria-projeto. Use ao começar um projeto novo."
---

# Brainstorming de Projeto

Fase de exploração antes de decidir o que construir. O objetivo é sair com uma direção clara e testada, não com a primeira ideia que veio à cabeça.

## Como conduzir

1. **Verifique primeiro se já existe `memoria/brief.md`** (skill `memoria-projeto`) de uma sessão anterior sobre este mesmo projeto — se existir, parta dali em vez de recomeçar do zero. Se não houver nada registrado e o problema não estiver claro, pergunte: qual problema isso resolve, para quem, e o que acontece hoje sem essa solução.
2. **Gere alternativas de verdade.** Liste de 3 a 5 abordagens plausíveis — incluindo sempre a opção "mais simples possível" (às vezes nem precisa construir nada, ou dá pra resolver com uma ferramenta pronta). Não convirja na primeira ideia.
3. **Questione a ideia inicial do usuário** pelo menos uma vez, de forma direta: "e se isso não for necessário porque X?" ou "o que quebra se a gente simplificar assim?".
4. **Avalie cada alternativa** rapidamente: complexidade, risco, tempo até ter algo funcionando.
5. **Convirja.** Recomende uma direção com base nos critérios do usuário (por padrão aqui: dev único, quer estabilidade e segurança sem infra pesada), ou peça para ele escolher.

## Saída

Feche com um **Brief de Decisão** curto:

- Problema
- Alternativas consideradas (e por que descartadas)
- Direção escolhida
- Riscos/pendências em aberto

Grave esse brief em `memoria/brief.md` via `memoria-projeto` (além de deixá-lo na conversa). Termine perguntando se o usuário quer seguir para a modelagem do domínio (skill `ddd-modeling`).