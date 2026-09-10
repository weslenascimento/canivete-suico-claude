---
name: frontend-quality
description: "Governa qualidade de UI/UX em frontends existentes: design system, hierarquia, responsividade, estados, acessibilidade e fidelidade visual sem alterar regras de negócio. Use ao criar ou revisar telas."
---

# Frontend Quality

Combina disciplina de design system com revisão estética. Não substitui requisitos nem regras de negócio.

1. Antes de alterar uma tela, leia componentes, tokens, layouts e padrões existentes.
2. Preserve comportamento e regras de negócio; mudança visual não autoriza mudança funcional.
3. Reutilize componentes e tokens antes de criar variantes novas.
4. Garanta hierarquia visual clara: ação primária inequívoca, densidade coerente e alinhamento consistente.
5. Evite aparência genérica gerada por IA: excesso de cards, gradientes decorativos, sombras sem função, textos artificiais e componentes diferentes para o mesmo conceito.
6. Verifique desktop e mobile; layouts não devem saltar de tamanho entre loading, empty e populated sem necessidade.
7. Trate estados: loading, empty, error, success, disabled, permission denied e ações em andamento quando aplicáveis.
8. Verifique navegação por teclado, foco, labels, contraste e semântica básica.
9. Para tabelas e telas densas, priorize leitura, comparação, filtros e ações sem deslocamentos inesperados de layout.
10. Quando houver referência visual aprovada, trate-a como requisito e compare a implementação contra ela.

## Saída

Checklist pass/fail com divergências funcionais separadas das divergências visuais. Não declare aprovado sem verificar os estados relevantes.