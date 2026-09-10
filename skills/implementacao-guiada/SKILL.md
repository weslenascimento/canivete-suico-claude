---
name: implementacao-guiada
description: "Governa a escrita do código durante a implementação: só constrói o que está na spec, confere nomes contra o glossário de domínio, declara o raio de alteração e delega testes/UI/debug às skills especializadas. Use entre template-projeto e harness."
---

# Implementação Guiada por Spec

Fase entre `template-projeto` e `harness`: governa a escrita do código em si. Seu papel é controlar escopo, aderência à spec, coerência com o domínio e o raio de alteração. Não deve duplicar testing strategy, debugging, revisão ou validação final.

## Responsabilidade desta skill

- garantir que só seja implementado o que está na spec;
- conferir linguagem ubíqua e contratos já definidos;
- declarar e controlar o raio de alteração;
- implementar em passos pequenos e reversíveis;
- registrar decisões de implementação.

## O que deve ser delegado

- estratégia de testes → `testing-strategy`;
- bug/comportamento inesperado → `debug`;
- qualidade visual e consistência de interface → `frontend-quality`;
- revisão técnica independente → `code-review`;
- verificação final contra a spec → `harness`.

## Como conduzir

1. **Carregue a spec e o glossário de domínio antes de escrever qualquer código** — via `memoria-projeto` (`spec.md`, `dominio.md`) se existirem, ou pedindo às skills `spec-driven`/`ddd-modeling`. Nunca confie apenas na memória da conversa.
2. **Implemente exclusivamente o que está nos critérios de aceitação.** Necessidade não prevista vira decisão explícita; nunca amplie o escopo silenciosamente.
3. **Confira entidades, campos, rotas, eventos e comandos contra a linguagem ubíqua e contratos existentes.** Conceito novo ou contraditório exige confirmação/atualização da spec ou domínio antes de seguir.
4. **Declare o raio de alteração antes de editar:** arquivos/módulos previstos e motivo. Alteração fora do raio exige justificativa explícita e atualização do registro.
5. **Defina evidência antes do código.** Para comportamento relevante ou com risco de regressão, invoque `testing-strategy` para mapear critério → teste/evidência. Não replique aqui a estratégia de cobertura.
6. **Implemente em incrementos pequenos.** Evite refatorações paralelas, troca de biblioteca e limpeza cosmética fora do escopo.
7. **Se a tarefa for correção de defeito**, use `debug` antes da correção para reproduzir/isolar a causa. A implementação aplica apenas a correção diagnosticada.
8. **Ao alterar interface**, preserve componentes/tokens existentes e use `frontend-quality` para critérios específicos de design, responsividade, estados e acessibilidade. Mudança visual não autoriza mudança de regra de negócio.
9. **Registre em `memoria/implementacao.md`** o raio real, decisões relevantes, desvios justificados e evidências produzidas.
10. Ao terminar o BUILD, encaminhe para `harness`. `code-review` deve ser chamado pelo harness ou explicitamente antes dele quando o risco justificar.

## Saída

Registro curto contendo:

- critérios implementados;
- arquivos/módulos alterados;
- desvios do raio inicialmente declarado;
- decisões de implementação;
- testes/evidências já produzidos;
- pendências conhecidas.
