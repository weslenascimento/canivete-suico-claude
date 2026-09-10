---
name: deploy-checklist
description: "Executa o go/no-go de entrega verificando testes, migrações, configuração, compatibilidade, rollback e observabilidade proporcional ao risco. Use imediatamente antes de deploy/release."
---

# Deploy Checklist

1. Spec e critérios de aceitação verificados.
2. Suíte completa, lint e type-check aplicáveis aprovados.
3. Migrações revisadas quanto a ordem, locks, compatibilidade e reversão.
4. Variáveis/configuração/secrets necessários identificados sem expor valores sensíveis.
5. Compatibilidade com consumidores e versões anteriores avaliada.
6. Estratégia de rollback definida para mudanças de risco relevante.
7. Feature flag/canary somente quando trouxer benefício real.
8. Logs, métricas e alertas suficientes para detectar falha pós-deploy.
9. Smoke test pós-deploy definido para fluxos críticos.

## Saída

GO somente se não houver bloqueante conhecido. Caso contrário, NO-GO com os itens objetivos que precisam ser resolvidos.