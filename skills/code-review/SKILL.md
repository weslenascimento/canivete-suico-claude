---
name: code-review
description: "Revisa alterações de código procurando bugs, regressões, violações da spec, segurança, contratos e complexidade desnecessária. Use depois da implementação e antes de ship/deploy."
---

# Code Review

Revise primeiro por correção, depois por qualidade.

1. Compare a mudança com a spec e o raio de alteração declarado.
2. Procure comportamento incorreto, edge cases, regressões e alterações fora de escopo.
3. Verifique autenticação/autorização, isolamento de dados, validação de entrada, segredos e exposição indevida.
4. Verifique contratos de API/eventos/schema e compatibilidade.
5. Confirme tratamento de erros, idempotência e concorrência quando aplicáveis.
6. Avalie testes: eles realmente falhariam se o comportamento estivesse errado?
7. Só depois avalie legibilidade, duplicação e simplificação.
8. Não proponha refatorações cosméticas sem benefício concreto para a mudança.

## Saída

Liste achados por severidade (bloqueante, importante, melhoria), com arquivo/local, impacto e correção sugerida. Se não houver achados materiais, diga isso explicitamente.