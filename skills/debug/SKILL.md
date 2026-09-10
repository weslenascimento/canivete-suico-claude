---
name: debug
description: "Executa debugging sistemático: reproduzir, coletar evidências, isolar causa, formular hipótese, corrigir minimamente e provar ausência de regressão. Use diante de bug, teste falhando ou comportamento inesperado."
---

# Debug Sistemático

1. Não corrija antes de reproduzir ou obter evidência suficiente do defeito.
2. Registre esperado versus observado e o caminho mínimo de reprodução.
3. Inspecione logs, stack trace, estado, entradas e fronteiras envolvidas.
4. Reduza o problema até localizar a primeira divergência observável.
5. Formule uma hipótese de causa raiz e tente refutá-la antes de editar.
6. Quando viável, crie teste que falha pelo motivo correto.
7. Faça a menor correção possível; não refatore componentes adjacentes sem necessidade.
8. Rode o teste de reprodução, testes relacionados e depois a suíte inteira.
9. Documente causa raiz, correção e evidência de verificação.

Se não houver evidência suficiente para afirmar causa raiz, diga explicitamente que o diagnóstico permanece inconclusivo.