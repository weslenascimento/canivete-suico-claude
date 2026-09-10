---
name: canivete-suico
description: "Conduz um projeto solo do zero ao deploy encadeando brainstorming → DDD → spec-driven → template → implementação guiada → harness, usando skills especializadas de arquitetura, testes, debug, UI, review e deploy quando necessário."
---

# Canivete Suíço — Fluxo de Projeto Solo

Conduz um projeto do zero (ou de qualquer ponto) pelas seis fases principais:

Brainstorming → DDD → Spec-Driven → Template de Projeto → Implementação Guiada → Harness

As skills `architecture`, `system-design`, `testing-strategy`, `debug`, `frontend-quality`, `code-review` e `deploy-checklist` são **capacidades especializadas**, chamadas sob demanda dentro do fluxo. Elas não são novas fases obrigatórias.

## Princípio: diagnóstico ativo, nunca autoavaliação do usuário

Nunca pergunte ao usuário algo que exige que ele já entenda o próprio fluxo para responder. Primeiro leia memória, código e evidências existentes; só pergunte o que não puder ser inferido com segurança, usando perguntas concretas e verificáveis.

## Como conduzir

1. **Diagnostique a fase pela memória do projeto e pelos artefatos existentes.** Verifique `memoria/` e identifique o ponto mais avançado realmente concluído:
   - nada definido → `brainstorming`;
   - ideia definida, domínio ausente → `ddd-modeling`;
   - domínio definido, spec ausente → `spec-driven`;
   - spec definida, estrutura/template ausente → `template-projeto`;
   - estrutura pronta e implementação em andamento → `implementacao-guiada`;
   - implementação concluída e falta verificação → `harness`.
2. **Diagnostique o porte por sinais concretos** e registre em `memoria/porte.md`:
   - pequeno: poucos módulos, baixa concorrência, um processo/serviço suficiente;
   - médio: uso contínuo, confiabilidade relevante, múltiplos processos/integrações possíveis, CI real esperado;
   - grande: múltiplos serviços/equipes, escala assíncrona, SLAs, múltiplos ambientes, IaC/orquestração/observabilidade.
   O porte nunca é escolhido por ambição arquitetural.
3. **Use `architecture` somente para decisões estruturais relevantes ou difíceis de reverter.** Para sistemas distribuídos/integrações com requisitos de escala e falha, use `system-design`.
4. **Execute as fases principais em ordem**, usando `memoria-projeto` para persistir o artefato de cada uma.
5. **Checkpoint entre fases:** mostre o artefato produzido e aguarde aprovação antes de avançar para a próxima fase principal.
6. Durante `implementacao-guiada`:
   - use `testing-strategy` quando houver comportamento relevante, risco de regressão ou necessidade de definir cobertura;
   - use `debug` para defeitos/comportamentos inesperados antes da correção;
   - use `frontend-quality` para criação/revisão de interface.
7. Ao final do BUILD, execute `harness`. O harness reúne evidências e, quando necessário, aciona `testing-strategy`, `code-review`, `frontend-quality` ou `debug`.
8. **Somente após PASS no harness**, execute `deploy-checklist` para o GO/NO-GO operacional de release/deploy.
9. Em toda fase, calibre profundidade e infraestrutura pelo porte real. Segurança, correção e isolamento de dados não são reduzidos por porte.
10. Se memória e código divergirem, o código/evidência real prevalece e a memória deve ser atualizada.

## Modelo de responsabilidades

- `brainstorming`: decidir o que vale construir;
- `ddd-modeling`: linguagem e regras do domínio;
- `spec-driven`: definir comportamento verificável e não-objetivos;
- `template-projeto`: estrutura e identidade base;
- `implementacao-guiada`: controlar escopo e escrever código;
- `testing-strategy`: decidir como provar comportamento;
- `debug`: localizar causa raiz de defeitos;
- `frontend-quality`: garantir qualidade de interface sem alterar negócio;
- `architecture`: decisões arquiteturais/ADRs;
- `system-design`: desenho de sistemas e integrações;
- `code-review`: revisão técnica independente;
- `harness`: gate de verificação;
- `deploy-checklist`: gate operacional de release;
- `memoria-projeto`: persistência compacta das decisões.

## Quando usar skills isoladas

Se o usuário pedir apenas uma capacidade específica, use a skill correspondente diretamente. O `canivete-suico` é o orquestrador para fluxo completo ou quando o ponto de entrada precisa ser diagnosticado.
