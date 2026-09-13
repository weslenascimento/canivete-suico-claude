---
name: harness
description: "Orquestra a verificação final da implementação contra a spec, evidências, raio de alteração, UI/UX e regressões, delegando testes, review, debug e deploy às skills especializadas. Use ao final do BUILD e antes de ship/deploy."
---

# Harness — Orquestração de Verificação

O `harness` é o **gate de verificação**. Ele não redefine estratégia de testes, não faz debugging improvisado e não duplica code review ou checklist de deploy. Seu papel é reunir evidências, acionar as skills especializadas quando necessário e emitir um resultado PASS/FAIL e GO/NO-GO técnico para seguir ao SHIP.

## Responsabilidade desta skill

- verificar cada critério de aceitação da spec;
- conferir evidências produzidas;
- comparar alterações reais com o raio declarado;
- garantir anti-regressão;
- coordenar as verificações especializadas;
- registrar o estado final em `memoria/harness.md`.

## Skills especializadas chamadas pelo harness

- cobertura/estratégia de testes → `testing-strategy`;
- revisão técnica e segurança → `code-review`;
- falha de teste ou comportamento inesperado → `debug`;
- qualidade visual/interface → `frontend-quality`;
- preparação final de release/deploy → `deploy-checklist`.

## Como conduzir

1. **Carregue `memoria/spec.md`, `memoria/implementacao.md`, `memoria/porte.md` e a evidência disponível.** Se não houver spec, não invente critérios: extraia o mínimo observável necessário antes de validar.
2. **Monte uma matriz critério → evidência → status.** Para cada critério de aceitação, classifique `PASS`, `FAIL` ou `SEM EVIDÊNCIA`.
3. **Verifique cobertura suficiente.** Se faltar estratégia/evidência para comportamento relevante, invoque `testing-strategy`; o harness não redesenha os testes por conta própria.
4. **Execute/verifique anti-regressão.** Rode a suíte existente inteira quando houver automação. Teste antigo quebrado é bloqueante até diagnóstico ou decisão explícita registrada.
5. **Compare o diff real com o raio de alteração de `implementacao-guiada`.** Arquivo/módulo fora do raio precisa de justificativa registrada; alteração silenciosa fora de escopo bloqueia aprovação.
6. **Para código alterado com risco material**, invoque `code-review`. Achado bloqueante impede aprovação; achado importante precisa de decisão explícita antes de seguir.
7. **Para UI**, invoque/consulte `frontend-quality` e verifique estados relevantes, responsividade, consistência visual e ausência de alteração funcional indevida.
8. **Se qualquer teste ou comportamento falhar**, encaminhe para `debug`. Depois da correção, retome o harness desde os critérios afetados e repita a suíte de regressão.
9. **Calibre a exigência pelo porte**, sem reduzir segurança:
   - pequeno: checklist/manual é aceitável onde não há suíte, desde que haja evidência objetiva;
   - médio: CI e testes automatizados para comportamentos relevantes são padrão;
   - grande: pipeline automatizado, contratos e observabilidade fazem parte do gate.
10. **Registre em `memoria/harness.md`** a matriz final, regressões verificadas, findings de review, pendências e decisão.
11. Se o resultado for PASS e não houver bloqueantes, encaminhe para `deploy-checklist`. O deploy checklist é quem emite o GO/NO-GO operacional de release.

## Saída

Resumo objetivo contendo:

- critérios: PASS/FAIL/SEM EVIDÊNCIA;
- suíte de regressão: PASS/FAIL/NÃO APLICÁVEL;
- raio de alteração: CONFORME/DIVERGENTE;
- code review: SEM BLOQUEANTES/COM BLOQUEANTES/NÃO APLICÁVEL;
- UI/UX: PASS/FAIL/NÃO APLICÁVEL;
- decisão do harness: **PASS** ou **FAIL**;
- próxima ação: `deploy-checklist`, `debug`, ajuste de implementação ou atualização de spec.
