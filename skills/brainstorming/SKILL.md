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

## Controle de convergência e escopo (BRN-01 a BRN-04)

Estas regras são obrigatórias em todo brainstorming e complementam — sem substituir — "Como conduzir" e "Apresentação das perguntas e registro de decisões". A meta é chegar a decisões suficientes para o fluxo principal, não maximizar a quantidade de perguntas.

### BRN-01 — Convergência progressiva e backlog

- **Avalie a suficiência continuamente**, especialmente depois de cada decisão macro: ainda falta alguma regra essencial para definir o resultado e avançar sem inventar uma decisão crítica?
- **Identifique ativamente excessos**: detalhes prematuros, novas funcionalidades, variantes remotas, exceções não bloqueantes e ramificações que ampliem o escopo sem alterar o fluxo essencial.
- **Não transforme excessos em novas perguntas obrigatórias.** Encaminhe-os a um backlog para retomar quando oportuno, preservando contexto, motivação e vínculo com o tema/decisão de origem.
- **Não descarte ideias.** Registre no backlog sem tratá-las como aprovadas ou incluídas no MVP.

### BRN-02 — Classificação inteligente de cada questão

Antes de perguntar, avalie **relevância**, **necessidade imediata**, **impacto no MVP**, **dependências** e **fase adequada**. Classifique internamente toda questão potencial como:

1. **Decisão obrigatória agora:** sem a resposta, há bloqueio real para definir o fluxo principal ou uma regra de negócio essencial. Pergunte, uma por vez, no formato A–E.
2. **Definição posterior:** pertence a Domain Discovery, DDD, Spec-Driven ou implementação e não bloqueia a descoberta macro. Registre para a fase correta; não antecipe o detalhamento.
3. **Backlog de evolução:** melhoria opcional, automação futura, exceção não crítica ou expansão funcional. Registre com contexto para discussão futura; não amplie o escopo atual.

Importância não implica urgência. Se algo for relevante, mas não bloqueante, não é motivo suficiente para prolongar o brainstorming.

### BRN-03 — Controle inteligente de profundidade

- Antes de **cada nova pergunta**, verifique se sua resposta realmente muda o fluxo principal, resolve dependência essencial ou elimina ambiguidade bloqueante.
- Detecte repetição de decisões, pequenas variações do mesmo assunto, aprofundamento prematuro e ramificações em cadeia.
- **Interrompa** perguntas sem impacto concreto; direcione os pontos aproveitáveis ao backlog ou à fase posterior.
- Não imponha um número rígido de perguntas: um tema complexo pode exigir aprofundamento legítimo, desde que cada questão tenha necessidade demonstrável.
- Não abra uma nova rodada de perguntas apenas porque é possível imaginar outros cenários.

### BRN-04 — Encerramento assistido e checkpoint

Quando objetivo, atores, fluxo principal, limites de escopo e regras essenciais estiverem suficientemente claros:

1. **Pare de propor novas perguntas exploratórias.** Não crie uma pergunta final artificial para estender a sessão.
2. **Apresente um diagnóstico de suficiência**, explicando brevemente o que já permite avançar e identificando somente lacunas realmente bloqueantes, se existirem.
3. **Consolide** decisões confirmadas e complementos, separando explicitamente **pendências bloqueantes**, **definições posteriores** e **backlog de evolução**, sem promover itens pendentes a decisões aprovadas.
4. **Recomende o encerramento** da descoberta macro e a transição à próxima fase compatível com o fluxo do projeto.
5. **Peça confirmação ao usuário** para encerrar, revisar um ponto específico ou continuar por motivo concreto. Respeite a escolha; se continuar, investigue só o que estiver justificado, preservando as regras de controle de escopo.

A revisão de suficiência pode acontecer antes de todas as questões inicialmente imaginadas terem sido exploradas. O encerramento depende da suficiência de decisões, não da contagem de perguntas.

**Critério prático para propor outra pergunta:** "Se esta resposta não vier agora, ainda conseguiremos consolidar a descoberta macro e prosseguir sem inventar uma regra essencial?" Se **sim**, registre como posterior/backlog e **não pergunte agora**. Se **não**, explique o bloqueio e formule uma única pergunta no formato aprovado.

**Registro mínimo de backlog:** identificador ou título, descrição/contexto, razão do adiamento, origem (pergunta/decisão relacionada), fase sugerida e status "não decidido". Disponibilize-o no resumo/checkpoint e preserve para retomada posterior via `memoria-projeto`, quando houver persistência disponível.

## Saída

Feche com um **Brief de Decisão** curto:

- Problema
- Alternativas consideradas (e por que descartadas)
- Direção escolhida
- Riscos/pendências em aberto

Grave esse brief em `memoria/brief.md` via `memoria-projeto` (além de deixá-lo na conversa). Termine perguntando se o usuário quer seguir para a modelagem do domínio (skill `ddd-modeling`).