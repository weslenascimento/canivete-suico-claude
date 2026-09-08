# Canivete Suíço — Claude para Dev Solo

Um plugin de skills para o [Claude](https://claude.ai) que conduz um projeto de software, sozinho, do zero ao deploy — com disciplina de processo em vez de infraestrutura pesada. Pensado para quem desenvolve sozinho e quer previsibilidade, segurança e estabilidade sem "usar uma bazuca pra matar uma mosca".

## O fluxo

```
brainstorming → ddd-modeling → spec-driven → template-projeto → implementacao-guiada → harness
                                        (tudo passa por memoria-projeto)
```

| Fase | Skill | O que faz |
|---|---|---|
| 1 | `brainstorming` | Explora o problema antes de decidir o que construir: gera alternativas reais, questiona a ideia inicial, converge numa direção. |
| 2 | `ddd-modeling` | Modela o domínio com DDD (linguagem ubíqua, bounded contexts, entidades e agregados), calibrado pelo porte do projeto. |
| 3 | `spec-driven` | Transforma o domínio numa spec verificável: casos de uso, critérios de aceitação, contratos, não-objetivos e pilares de UI/UX obrigatórios. |
| 4 | `template-projeto` | Aplica ou cria um template de ponta a ponta (estrutura de código + tema visual), reaproveitado entre projetos do mesmo porte. |
| 5 | `implementacao-guiada` | Governa a escrita do código: só implementa o que está na spec, confere nomes contra o glossário de domínio (evita alucinação), declara o raio de alteração. |
| 6 | `harness` | Verifica a implementação contra a spec, roda a suíte de testes inteira (anti-regressão), e escala a automação conforme o porte. |

A skill `canivete-suico` é o orquestrador: encadeia as seis fases, com checkpoint entre cada uma. A skill `memoria-projeto` é o "cérebro" persistente — mantém tudo em arquivos `.md` simples com `[[wikilinks]]`, dentro de uma pasta `memoria/` no projeto.

## Princípios de design

- **Diagnóstico ativo, nunca autoavaliação do usuário.** Nenhuma skill pergunta algo que exige que você já entenda o próprio fluxo para responder ("em qual fase você está?", "isso é pequeno ou grande?"). Elas descobrem isso sozinhas — pela memória do projeto, ou por perguntas concretas e verificáveis.
- **Anti-bazuca.** Automação pesada (CI completo, filas, containers orquestrados, infraestrutura como código) só é sugerida quando o porte do projeto realmente pede — nunca por padrão, nunca por "parecer mais profissional".
- **Memória persistente, custo zero de token.** Cada fase lê e grava um resumo compacto em `memoria/`, em vez de exigir que o Claude releia o projeto inteiro (ou você reexplique tudo) a cada nova pergunta. Os arquivos são `.md` puro com `[[wikilinks]]` — navegáveis por qualquer app gratuito de notas linkadas (recomendado: [Foam](https://foambubble.github.io/foam/), extensão gratuita e open source do VS Code; também funciona com Logseq, Obsidian, ou nenhum app).
- **Porte como diagnóstico, não escolha.** Pequeno, médio ou grande é definido por sinais concretos (número de usuários, precisa de mais de um serviço, exige fila/Kafka/Kubernetes/Terraform etc.), registrados em `memoria/porte.md`, e usado para calibrar toda decisão adiante.
- **Guardas contra os erros mais comuns de código gerado por IA:** gerar coisa não pedida (não-objetivos explícitos na spec + implementação restrita a ela), alucinação de domínio (checagem contra o glossário de linguagem ubíqua), e regressão (harness roda a suíte de testes inteira, não só a nova, a cada verificação).

## Instalação

### Como plugin do Cowork / Claude Code

Baixe ou clone este repositório e instale a pasta como plugin, ou arraste o arquivo `.plugin` (quando publicado como release) na conversa do Claude.

### Manual (copiar as skills)

Copie o conteúdo de `skills/` para a pasta de skills da sua conta Claude (cada subpasta já tem seu `SKILL.md`).

## Uso

Para começar um projeto novo do zero:

```
/canivete-suico
```

Para usar uma fase isolada (ex: só modelar o domínio de algo que já existe):

```
/ddd-modeling
```

## Estrutura do repositório

```
canivete-suico-claude/
├── .claude-plugin/
│   └── plugin.json
├── skills/
│   ├── brainstorming/SKILL.md
│   ├── ddd-modeling/SKILL.md
│   ├── spec-driven/SKILL.md
│   ├── template-projeto/SKILL.md
│   ├── implementacao-guiada/SKILL.md
│   ├── harness/SKILL.md
│   ├── memoria-projeto/SKILL.md
│   └── canivete-suico/SKILL.md
└── README.md
```

## Licença

MIT — use, adapte e redistribua livremente.
