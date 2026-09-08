---
name: implementacao-guiada
description: "Governa a escrita do código durante a implementação: só constrói o que está na spec, confere nomes contra o glossário de domínio e a UI contra o template visual antes de gerar, e declara o raio de alteração. Use entre template-projeto e harness."
---

# Implementação Guiada por Spec

Fase entre `template-projeto` e `harness`: governa a escrita do código em si, para evitar problemas comuns em código gerado por IA — gerar coisa não pedida, gerar coisa sem relação com o domínio (alucinação), mexer fora do escopo necessário, e quebrar a consistência visual do projeto.

## Como conduzir

1. **Carregue a spec e o glossário de domínio antes de escrever qualquer código** — via `memoria-projeto` (`spec.md`, `dominio.md`) se existirem, ou pedindo à skill `spec-driven`/`ddd-modeling` diretamente. Nunca confie só na memória da conversa para isso; releia os artefatos.
2. **Implemente exclusivamente o que está nos critérios de aceitação da spec.** Se perceber que algo a mais parece necessário, isso vira uma pergunta explícita ao usuário ("percebi que X pode ser necessário, mas não está na spec — incluo ou fica pra depois?") — nunca uma adição silenciosa.
3. **Confira cada entidade/campo/rota gerado contra o glossário da linguagem ubíqua** (`dominio.md`). Se for gerar algo sobre um conceito que não está no glossário (ex: pediram "pessoa" e o código está tratando "peça"), pare e confirme antes de continuar — isso é sinal de alucinação, não de criatividade.
4. **Ao gerar qualquer interface**, use os tokens/tema definidos em `template.md` (skill `template-projeto`) — cores, tipografia, componentes — em vez de inventar estilo novo por tela, para manter a consistência visual.
5. **Declare o raio de alteração antes de mexer**: liste quais arquivos/módulos serão tocados para atender o critério de aceitação em questão. Qualquer alteração fora dessa lista precisa de justificativa explícita, não pode acontecer "de passagem".
6. Registre o raio de alteração e as decisões tomadas em `memoria-projeto` (`implementacao.md`).
7. Ao final, encaminhe para `harness` para a verificação.

## Saída

Um registro curto do raio de alteração (arquivos tocados e por quê) e de qualquer decisão de implementação tomada — alimenta a skill `harness`.