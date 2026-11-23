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


## Apresentação das perguntas e registro de decisões

Ao conduzir a descoberta com decisões sucessivas, siga obrigatoriamente este formato:

1. **Uma pergunta por vez.** Apresente o identificador da decisão (quando houver), o contexto, o problema e uma única pergunta objetiva. Não antecipe a próxima decisão.
2. **Alternativas A–E.** Ofereça quatro abordagens plausíveis e distintas, identificadas por **A**, **B**, **C** e **D**, com descrição breve de impactos ou diferenças. Inclua **E — Outra abordagem**, para o usuário propor um caminho próprio. Preserve entre A–D a abordagem mais simples possível. A letra D não precisa ser híbrida: use modelo híbrido somente quando fizer sentido.
3. **Recomendação fundamentada.** Indique a alternativa recomendada e a razão, considerando complexidade, riscos, estabilidade, segurança e tempo para gerar valor. A recomendação não é uma decisão automática.
4. **Campo de complemento sempre visível.** Apresente **em toda pergunta** um campo de texto livre, identificado como **"Complemento da alternativa selecionada (opcional)"**. O campo deve estar disponível para **qualquer** alternativa A, B, C, D ou E, e permanecer visível mesmo sem seleção ou quando a seleção mudar. Ele aceita condições, exceções, ressalvas, ajustes e, para E, a descrição da proposta alternativa. **Não condicione a exibição do campo à escolha de E ou ao preenchimento prévio.**
5. **Interação conforme a interface.** Se o ambiente suportar controles interativos, utilize seleção exclusiva para A–E, campo de texto multilinha persistente durante a escolha e botão de confirmação (por exemplo, **"Aprovar alternativa e continuar"**). Se não suportar esses controles, apresente explicitamente **"Complemento (opcional):"** com espaço/instrução para resposta livre no mesmo bloco da pergunta; não finja que existe um campo interativo.
6. **Confirmação e progressão.** Apenas após confirmação explícita do usuário registre a alternativa escolhida **junto com o complemento integral**, inclusive quando vazio, e avance para a próxima pergunta. Não descarte, resuma alterando o significado, nem interprete o complemento silenciosamente. Se o complemento conflitar com a alternativa, peça esclarecimento antes de consolidar.
7. **Rastreabilidade.** Mantenha o identificador da pergunta, a alternativa selecionada, o complemento literal, o status de aprovação e eventuais pendências. Preserve decisões anteriores e a distinção entre recomendação e aprovação.

**Modelo de cada pergunta:** identificação → contexto → pergunta → alternativas A–E → recomendação justificada → campo de complemento livre (opcional, sempre visível) → confirmação. Esse formato não substitui a investigação e o questionamento crítico definidos em "Como conduzir"; apenas padroniza a interação e a captura das decisões.

## Saída

Feche com um **Brief de Decisão** curto:

- Problema
- Alternativas consideradas (e por que descartadas)
- Direção escolhida
- Riscos/pendências em aberto

Grave esse brief em `memoria/brief.md` via `memoria-projeto` (além de deixá-lo na conversa). Termine perguntando se o usuário quer seguir para a modelagem do domínio (skill `ddd-modeling`).