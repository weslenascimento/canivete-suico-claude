---
name: canivete-suico
description: "Conduz um projeto solo do zero ao deploy encadeando brainstorming → DDD → spec-driven → template → implementação guiada → harness, diagnosticando memória, fase e porte por sinais concretos antes de perguntar ao usuário. Use ao começar um projeto novo do zero."
---

# Canivete Suíço — Fluxo de Projeto Solo

Conduz um projeto do zero (ou de qualquer ponto) pelas seis fases: Brainstorming → DDD → Spec-Driven → Template de Projeto → Implementação Guiada → Harness. É o ponto de entrada para "começar um projeto novo do jeito certo", encadeando as skills de fase e carregando o contexto de uma para a outra via `memoria-projeto`.

## Princípio: diagnóstico ativo, nunca autoavaliação do usuário

Nunca pergunte ao usuário algo que exige que ele já entenda o próprio fluxo para responder (ex: "em qual fase você está?", "isso é pequeno, médio ou grande?"). Essa é uma responsabilidade da skill, não dele. Primeiro tente responder isso sozinho lendo o que já existe; só pergunte ao usuário o que não dá pra descobrir sozinho, e sempre com perguntas concretas e verificáveis, nunca com julgamentos abertos.

## Como conduzir

1. **Diagnostique a fase primeiro pela memória do projeto, depois por perguntas concretas.** Verifique se existe a pasta `memoria/` (skill `memoria-projeto`). Se existir, leia os arquivos para saber em que fase o projeto já está. Se não existir (ou for projeto novo), diagnostique:
   - Existe alguma ideia escrita ou documento sobre isso, ou está tudo só na cabeça? → se nada, comece em `brainstorming`.
   - Já existem entidades, regras de negócio ou um "vocabulário" do domínio definidos, mesmo informalmente? → se não, `ddd-modeling` é o próximo passo.
   - Existe uma spec, critérios de aceitação ou requisitos escritos (formais ou não)? → se não, siga para `spec-driven`.
   - Já existe uma estrutura/template aplicado ao projeto? → se não, siga para `template-projeto`.
   - Já existe código e/ou testes implementando isso? → se está sendo escrito agora, o ponto de entrada é `implementacao-guiada`; se já está pronto e só falta verificar, é `harness`.
2. **Diagnostique o porte por sinais concretos** (registre em `memoria/porte.md`, via `memoria-projeto`), nunca perguntando "isso é pequeno, médio ou grande?":
   - **Pequeno**: poucos módulos, não espera mais que dezenas de usuários simultâneos, não precisa rodar em mais de um processo/serviço, vida útil curta ou incerta. → um bounded context, contratos mínimos, harness em nível de checklist, zero infra externa (fila, containers orquestrados) a menos que peçam explicitamente.
   - **Médio**: uso contínuo esperado por meses/anos, número relevante de usuários simultâneos, precisa de disponibilidade/confiabilidade (não pode cair sem ninguém perceber), pode envolver mais de um serviço/processo. → contratos de API mais formais, `engineering:testing-strategy` e `engineering:deploy-checklist` passam a ser padrão, CI real, infra gerenciada simples (banco gerenciado, fila gerenciada) SE o caso de uso realmente pedir.
   - **Grande**: múltiplas equipes ou serviços independentes, processamento assíncrono em escala (fila tipo RabbitMQ/Kafka), precisa de infraestrutura como código (Terraform) e orquestração de containers (Kubernetes), SLAs formais, múltiplos ambientes com pipelines de promoção. → múltiplos bounded contexts legítimos, `engineering:system-design`/`engineering:architecture` a cada decisão relevante, harness escala para pipeline completo + IaC + observabilidade.
   - O porte nunca é escolhido por ambição ("fica mais profissional") — só pelos sinais acima. Ele pode mudar durante o projeto; se os sinais mudarem, rediagnostique, não trave na classificação inicial.
3. **Explique as 6 fases e o porte diagnosticado em uma frase cada**, como contexto, só depois dos diagnósticos — nunca como pergunta para o usuário decidir sozinho.
4. **Anuncie a fase e o porte escolhidos e o porquê**, com base nos diagnósticos. O usuário pode discordar e corrigir — mas a decisão inicial parte do diagnóstico, não de uma pergunta aberta.
5. Invoque as skills de fase em sequência: `brainstorming` → `ddd-modeling` → `spec-driven` → `template-projeto` → `implementacao-guiada` → `harness`, usando `memoria-projeto` para persistir e passar adiante o artefato de cada uma.
6. **Checkpoint entre fases:** depois de cada fase, mostre o artefato produzido e pergunte se o usuário quer seguir, ajustar, ou parar por ali. Nunca encadeie as fases sem pausa.
7. Em toda fase, calibre pelo porte diagnosticado — nunca aplique automação pesada a um projeto pequeno, nem deixe um projeto grande sem a estrutura que ele realmente precisa.
8. Essa skill pode ser chamada no meio de um projeto já em andamento, não só no início — nesse caso, os diagnósticos dos passos 1 e 2 (memória/sinais primeiro, perguntas depois) decidem onde entrar.

## Quando usar as skills soltas em vez desta

Se o usuário só quer uma fase isolada (ex: "me ajuda a modelar o domínio disso"), use a skill da fase diretamente em vez desta. Esta skill é para quando ele quer o fluxo completo ou não sabe por onde começar.