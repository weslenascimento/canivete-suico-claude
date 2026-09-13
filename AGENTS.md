# Engineering Agent Stack

Este repositório usa um fluxo de engenharia orientado a especificação, domínio, verificação e mudanças mínimas.

## Regras operacionais

1. Leia primeiro o contexto persistente do projeto (`memoria/`) e os arquivos diretamente afetados.
2. Não presuma requisitos. Quando houver ambiguidade relevante, identifique-a explicitamente antes de codificar.
3. Faça a menor alteração capaz de satisfazer a spec. Não inclua melhorias laterais silenciosamente.
4. Preserve nomes, padrões e arquitetura já existentes, salvo quando a spec exigir mudança.
5. Antes de editar, declare o raio de alteração: arquivos/módulos esperados e motivo.
6. Nunca declare uma tarefa concluída sem evidência verificável: testes, execução, logs ou checklist.
7. Toda correção de bug deve partir de reprodução/diagnóstico antes da alteração.
8. Toda feature deve ter critérios de aceitação verificáveis. Quando houver suíte automatizada, prefira teste que falha antes da implementação e passa depois.
9. Rode a suíte existente inteira antes de concluir, não apenas os testes novos.
10. Se um teste antigo quebrar, trate como regressão bloqueante até explicar e resolver.
11. Não introduza dependência, serviço, framework, fila, cache ou infraestrutura nova sem necessidade demonstrável.
12. Em UI, preserve o design system existente. Não invente uma estética diferente por tela.
13. Estados de loading, vazio, erro, sucesso, disabled e permissão devem ser considerados quando aplicáveis.
14. Segurança, isolamento de tenant, autorização, validação de entrada e exposição de dados são requisitos funcionais, não acabamento.
15. Atualize `memoria/` quando a implementação alterar decisões ou estado do projeto.

## Fluxo padrão

DEFINE → PLAN → BUILD → VERIFY → REVIEW → SHIP

- DEFINE: confirme problema, domínio, spec, critérios e não-objetivos.
- PLAN: descreva a estratégia e o raio de alteração.
- BUILD: implemente em passos pequenos e reversíveis.
- VERIFY: teste critérios novos e rode a suíte inteira.
- REVIEW: revise correção, simplicidade, segurança, regressões e consistência.
- SHIP: valide migrações, rollback, configuração e observabilidade necessárias.

## Princípios para agentes

- Simplicidade vence sofisticação não exigida.
- Código existente é evidência; inferências do agente não são.
- Uma mudança pequena e correta é preferível a uma refatoração ampla não solicitada.
- Explique suposições relevantes; não esconda incerteza atrás de implementação.
- Não trate warnings, falhas de lint, type-check ou testes como ruído sem investigar.
- Não altere contrato público sem tratar compatibilidade e consumidores.
- Não faça mudanças cosméticas em arquivos fora do escopo.

## Skills preferenciais

Use as skills conforme a necessidade:

- `brainstorming`
- `ddd-modeling`
- `spec-driven`
- `template-projeto`
- `implementacao-guiada`
- `testing-strategy`
- `debug`
- `architecture`
- `system-design`
- `frontend-quality`
- `code-review`
- `deploy-checklist`
- `harness`
- `memoria-projeto`
- `canivete-suico`

O `AGENTS.md` governa comportamento global. As skills detalham procedimentos especializados e devem ser carregadas apenas quando relevantes.