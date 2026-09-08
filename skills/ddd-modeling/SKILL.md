---
name: ddd-modeling
description: "Modela o domínio de um projeto com DDD (linguagem ubíqua, bounded contexts, entidades e agregados), extraindo o contexto por perguntas concretas e calibrando a profundidade pelo porte registrado em memoria-projeto. Use depois do brainstorming."
---

# Modelagem de Domínio (DDD)

Fase de estruturação: agora que já se sabe o que construir (via brainstorming ou já claro para o usuário), esta skill modela o domínio para orientar a spec e o código.

## Como conduzir

1. **Verifique primeiro `memoria/brief.md` e `memoria/dominio.md`** (skill `memoria-projeto`) — se existirem, parta dali. Senão, extraia o contexto com perguntas concretas, nunca com um pedido genérico de descrição: quais são as principais "coisas"/substantivos que esse sistema manipula (ex: pedido, cliente, pagamento)? quais ações/verbos acontecem sobre elas (ex: aprovar, cancelar, enviar)? quem realiza cada ação? Essas respostas já são a matéria-prima da linguagem ubíqua.
2. **Construa a linguagem ubíqua** a partir dessas respostas: defina cada substantivo/verbo com o usuário, em termos de negócio, não técnicos.
3. **Identifique bounded contexts calibrando pelo porte** (`memoria/porte.md`, via `memoria-projeto`): em projetos **pequenos**, o padrão é um único bounded context — só divida se houver de fato duas linguagens/regras conflitantes convivendo no mesmo termo. Em projetos **médios**, ainda prefira poucos contexts, mas com fronteiras mais formais. Em projetos **grandes**, múltiplos bounded contexts podem ser legítimos se refletirem equipes/serviços realmente independentes — nunca crie contextos por elegância acadêmica, em nenhum porte.
4. **Separe entidades de value objects**, e agrupe em **agregados** com as invariantes (regras que sempre precisam ser verdadeiras) explícitas.
5. **Calibre para o tamanho real do projeto.** Se o domínio é simples, o modelo deve ser simples — resista à tentação de aplicar DDD "de livro" em um CRUD pequeno, mesmo que o porte seja médio ou grande.
6. Se surgir uma decisão técnica relevante (ex: escolha de persistência, síncrono vs assíncrono, boundary de serviço), **não modele aqui** — sinalize para o usuário invocar `engineering:architecture` (ADR) ou `engineering:system-design`, que já cobrem isso.

## Saída

Feche com um resumo curto do modelo: entidades/agregados principais, bounded context(s), e as invariantes de negócio mais importantes. Grave em `memoria/dominio.md` via `memoria-projeto`. Esse resumo alimenta as skills `spec-driven` e `implementacao-guiada`.