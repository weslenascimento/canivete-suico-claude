---
name: testing-strategy
description: "Define a estratégia de testes proporcional ao risco e ao porte: unidade, integração, contrato, E2E e regressão, vinculando testes aos critérios de aceitação. Use ao planejar cobertura ou antes de implementar comportamento relevante."
---

# Testing Strategy

## Procedimento

1. Leia `memoria/spec.md`, `memoria/dominio.md` e a suíte existente.
2. Mapeie cada critério de aceitação para uma evidência verificável.
3. Use o teste mais barato que prova o comportamento: unidade para regra isolada; integração para fronteiras reais; contrato para APIs/eventos; E2E apenas para fluxos críticos.
4. Para bug, crie primeiro uma reprodução automatizada quando viável.
5. Para regra de negócio, cubra caminho feliz, limites e falhas relevantes.
6. Não busque percentual de cobertura como objetivo isolado; cubra risco e comportamento.
7. Preserve testes existentes e rode a suíte inteira no final.
8. Registre lacunas que permanecerem deliberadamente sem automação.

## Saída

Matriz curta: critério → tipo de teste → arquivo/cenário → status.