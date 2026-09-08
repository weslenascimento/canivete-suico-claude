---
name: harness
description: "Verifica a implementação contra a spec, o raio de alteração e os pilares de UI/UX, com anti-regressão (roda a suíte de testes inteira) e automação calibrada pelo porte do projeto. Use antes de cada deploy."
---

# Harness — Execução e Verificação

Verifica que a implementação atende à spec, com o nível de automação calibrado pelo porte do projeto (`memoria/porte.md`, diagnosticado em `canivete-suico`) — nunca por padrão fixo.

## Como conduzir

1. **Verifique com perguntas concretas, nunca perguntando abertamente o que significa "pronto".** Carregue a spec — via `memoria-projeto` (`spec.md`) se existir, ou da skill `spec-driven` — e, para cada critério de aceitação nela, pergunte diretamente: existe hoje algo (teste automatizado, execução manual, log) que confirme que isso funciona? Se não houver spec, extraia o mesmo por partes: o que precisa ser observavelmente verdade para você confiar que isso está pronto? — e construa o checklist a partir das respostas, nunca de uma definição abstrata dada de uma vez.
2. **Testes:** para cada critério de aceitação da spec, confirme que existe um teste (automatizado, se já há suíte; checklist manual, se não há). Em porte **pequeno**, checklist manual basta; em **médio**, `engineering:testing-strategy` passa a ser padrão, não exceção; em **grande**, cobertura automatizada é esperada antes do deploy.
3. **UI/UX:** para cada caso de uso com interface, confira contra os critérios definidos em `spec-driven` — consistência visual (usa o tema de `template.md`), responsividade (telas pequena e grande) e usabilidade básica (estados de carregamento/erro/sucesso visíveis). Isso é checklist manual em qualquer porte, a menos que o projeto já tenha testes visuais automatizados.
4. **Anti-regressão:** antes de considerar concluído, rode *toda* a suíte de testes já existente, não só a nova — um teste antigo quebrando é tão bloqueante quanto um critério novo sem cobertura. Compare o que foi de fato alterado com o raio de alteração declarado em `implementacao-guiada` (`memoria-projeto`/`implementacao.md`): qualquer arquivo tocado fora dessa lista precisa de justificativa explícita antes do deploy.
5. **Qualidade/segurança do código:** para o código alterado, aponte para `engineering:code-review` (ou Qodo, se instalado) em vez de reimplementar revisão de código aqui.
6. **Checklist de deploy:** reaproveite `engineering:deploy-checklist` para o go/no-go (migrações, plano de rollback, feature flags) em vez de duplicar essa lista.
7. **Se algo quebrar:** direcione para `engineering:debug` (reproduzir, isolar, diagnosticar, corrigir) em vez de improvisar debug aqui.
8. Registre o resultado da verificação em `memoria-projeto` (`harness.md`).

## Escala de infra por porte (substitui a regra anti-bazuca genérica)

- **Pequeno**: checklist manual, zero infra externa. Nada de fila, container orquestrado ou IaC a menos que o usuário peça explicitamente.
- **Médio**: CI real (não só checklist), infra gerenciada simples (banco gerenciado, fila gerenciada) SE o caso de uso pedir de verdade (ex: processamento assíncrono real).
- **Grande**: pipeline de CI completo, infraestrutura como código (Terraform), orquestração de containers (Kubernetes), observabilidade — deixa de ser exceção e vira padrão esperado.

Se o porte não estiver registrado em `memoria/porte.md`, trate como **pequeno** por padrão até haver diagnóstico — nunca escale por conta própria sem o porte confirmado.

## Saída

Um checklist curto de pass/fail contra os critérios de aceitação da spec (incluindo UI/UX), e uma nota de go/no-go para o deploy.