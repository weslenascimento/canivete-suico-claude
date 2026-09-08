---
name: memoria-projeto
description: "Mantém e lê a memória persistente de um projeto (brief, domínio, spec, porte, template, implementação, harness) como notas .md com wikilinks, compatível com Foam/Obsidian/Logseq. Use no início de qualquer fase do fluxo de projeto, para não reler tudo do zero."
---

# Memória de Projeto

Evita que cada nova pergunta ou implementação exija reler o projeto inteiro (código, histórico de conversa) do zero. Mantém um resumo compacto e persistente, em arquivos `.md` simples com `[[wikilinks]]` — legível por qualquer editor, e navegável com apps gratuitos como Foam (extensão do VS Code), Logseq ou Obsidian, sem exigir nenhum deles instalado.

## Onde mora

Uma pasta `memoria/` na raiz do projeto:

- `index.md` — ponto de entrada, linka para as notas abaixo.
- `brief.md` — saída da skill `brainstorming`.
- `dominio.md` — saída da skill `ddd-modeling` (linguagem ubíqua, agregados, invariantes).
- `porte.md` — classificação de porte (pequeno/médio/grande) e os sinais concretos que levaram a ela.
- `spec.md` — saída da skill `spec-driven` (casos de uso, critérios de aceitação, não-objetivos).
- `template.md` — saída da skill `template-projeto` (o que o template contém e onde vive).
- `implementacao.md` — saída da skill `implementacao-guiada` (raio de alteração, decisões tomadas durante o código).
- `harness.md` — saída da skill `harness` (checklist de verificação, estado atual).

## Como conduzir

1. **No início de qualquer fase** (chamada isolada ou dentro do `canivete-suico`): verifique se a pasta `memoria/` existe. Se existir, leia apenas os arquivos relevantes para a fase atual — nunca releia o código inteiro nem peça ao usuário para reexplicar o que já está registrado ali.
2. **Ao final de qualquer fase**: atualize (não duplique) o arquivo correspondente com o resultado produzido. Use `[[wikilinks]]` para conectar (ex: `spec.md` linkando `[[dominio]]` ao citar uma entidade).
3. **Se a memória não existir ainda**, crie a pasta e os arquivos conforme as fases forem produzindo resultado — não crie tudo de uma vez, vazio, no início.
4. **Se o conteúdo divergir do código real** (ex: a memória descreve uma regra que o código não implementa mais, ou um porte que já mudou), o real manda — atualize a memória, nunca finja que o registro antigo ainda vale.
5. **Se um arquivo crescer demais** para ser econômico de reler, divida por assunto (nunca por data) e mantenha `index.md` enxuto, só com links — não deixe conteúdo duplicado em dois lugares.
6. Isso é resumo de decisões, não documentação de usuário final nem substituto do código — não precisa de aprovação formal a cada atualização, mas deve ser revisável por humano a qualquer momento (por isso o formato simples, sem plugin obrigatório).

## Saída

Nenhuma saída própria — esta skill só mantém os arquivos que as outras fases produzem e leem.