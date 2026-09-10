# Validation Case — MCP Database Discovery

## Objetivo

Validar o Engineering Agent Stack em um caso real de alta ambiguidade técnica: um agente que se conecta a uma base inicialmente desconhecida e a transforma progressivamente em um domínio compreendido, consultável, explicável, auditável e reutilizável.

Este documento testa especificamente as skills `architecture` e `system-design`.

---

## Decisão arquitetural principal

O sistema deve separar explicitamente:

1. **Evidence** — fatos observáveis coletados do banco, consultas, amostras e metadados.
2. **Hypothesis** — interpretações inferidas a partir das evidências.
3. **Validation** — processo que tenta confirmar ou refutar uma hipótese.
4. **Knowledge** — conhecimento promovido após validação suficiente, sempre preservando proveniência e nível de confiança.

Regra central:

> Fato não é hipótese. Hipótese não vira conhecimento sem evidência rastreável.

---

## Arquitetura em camadas

### 1. Physical Discovery

Responsável apenas por observar o que existe fisicamente.

Descobertas típicas:
- tabelas e views;
- colunas e tipos;
- PK, FK e constraints;
- índices;
- nullability;
- defaults;
- cardinalidade aproximada;
- distribuição e amostras controladas de valores.

Saída: fatos técnicos com confiança 1.0 quando provenientes diretamente do metadata ou de consulta determinística.

### 2. Structural Inference

Responsável por detectar relacionamentos não declarados fisicamente.

Sinais possíveis:
- nomes de colunas semelhantes;
- sobreposição de valores;
- unicidade;
- cardinalidade observada;
- padrões de prefixo/sufixo;
- coocorrência em queries, procedures ou views;
- compatibilidade de tipos;
- frequência com que um valor de uma tabela aparece em outra.

Nenhum relacionamento inferido deve ser gravado como FK real ou tratado como verdade sem validação.

### 3. Semantic Discovery

Responsável por inferir significado de negócio.

Exemplos:
- `ALU001` pode representar Aluno;
- `RESP` pode representar Responsável;
- várias tabelas podem compor o conceito de Aluno;
- um campo pode ter semântica diferente do nome físico.

Fontes de evidência:
- nomes;
- valores;
- comentários do banco;
- procedures/views;
- queries de aplicação quando disponíveis;
- exemplos validados pelo usuário;
- padrões recorrentes entre tabelas.

### 4. Knowledge Layer

Persistência do conhecimento descoberto.

Deve armazenar:
- fatos;
- hipóteses;
- evidências de suporte e de refutação;
- score de confiança;
- status de validação;
- relações descobertas;
- glossário;
- consultas validadas;
- entidades de domínio descobertas;
- proveniência de cada conclusão.

---

## Modelo de confiança

A confiança não deve ser um único número mágico calculado pela LLM.

Cada hipótese deve ter componentes de evidência explicitáveis, por exemplo:

- metadata explícito;
- compatibilidade de tipos;
- overlap de valores;
- unicidade/cardinalidade;
- evidência em código/query;
- evidência semântica;
- confirmação humana.

O score agregado pode existir, mas deve ser derivado desses sinais e continuar auditável.

Exemplos:

```text
FK declarada no metadata
kind = FACT
confidence = 1.00

TB_MAT.CODALU ↔ ALU001.CODIGO
kind = INFERRED_RELATIONSHIP
confidence = 0.94
supports = [type_match, value_overlap, uniqueness]

ALU001 significa "Aluno"
kind = SEMANTIC_HYPOTHESIS
confidence = 0.82
supports = [column_names, sample_values, query_usage]
```

---

## Máquina de estados da hipótese

```text
DISCOVERED
   ↓
CANDIDATE
   ↓
UNDER_VALIDATION
   ├──→ REJECTED
   ├──→ INCONCLUSIVE
   └──→ VALIDATED
              ↓
          KNOWLEDGE
```

Uma hipótese rejeitada deve permanecer registrada com suas evidências para evitar que o agente proponha novamente a mesma interpretação sem novas evidências.

---

## Pipeline de descoberta

```text
Connect
  ↓
Inventory
  ↓
Profile
  ↓
Generate Evidence
  ↓
Generate Hypotheses
  ↓
Rank Hypotheses
  ↓
Validate
  ↓
Promote / Reject / Keep Inconclusive
  ↓
Update Knowledge Graph
  ↓
Use knowledge in next discovery cycle
```

O processo é iterativo. Conhecimento validado em um ciclo passa a ser contexto para o próximo.

---

## Componentes sugeridos

### Database Adapter

Abstrai SQL Server inicialmente, mas não deve vazar regras específicas para o restante do domínio.

Responsabilidades:
- metadata;
- queries somente leitura;
- profiling controlado;
- limites de execução;
- timeout;
- sanitização e escaping apropriados.

### Discovery Engine

Coordena descoberta física e coleta evidências.

Não interpreta domínio sozinho.

### Inference Engine

Gera candidatos estruturais e semânticos.

Pode combinar heurísticas determinísticas com LLM.

### Validation Engine

Executa testes que confirmam/refutam hipóteses.

Exemplos:
- overlap de chave;
- cardinalidade;
- ausência/presença de órfãos;
- joins candidatos;
- consistência temporal;
- validação cruzada por queries existentes.

### Knowledge Store

Persistência versionada e auditável.

Deve distinguir tipos de conhecimento e proveniência.

### Query Planner / Domain Query Layer

Usa apenas conhecimento validado ou explicitamente marcado como hipótese.

Quando uma resposta depender de hipótese não validada, isso deve aparecer na resposta ao usuário.

### Export Engine

Gera arquivos em layouts definidos a partir de consultas validadas e transformações versionadas.

Deve permitir reproduzir a geração e criar versões de correção.

---

## Caso crítico — banco mal modelado

O sistema não pode assumir que ausência de FK significa ausência de relacionamento.

Exemplo:

```text
ALU001
  CODIGO
  NOME

MATRI
  CODALU
  CURSO
```

Mesmo sem FK física, o sistema deve conseguir levantar a hipótese:

```text
MATRI.CODALU -> ALU001.CODIGO
```

E validá-la por evidências como:
- tipos compatíveis;
- `ALU001.CODIGO` altamente único;
- alto overlap dos valores;
- poucos ou nenhum órfão;
- cardinalidade N:1 observada;
- joins equivalentes encontrados em views/procedures/código quando disponíveis.

---

## Requisitos de segurança

- conexão preferencialmente read-only;
- deny-by-default para comandos destrutivos;
- limite de linhas e tempo por consulta de profiling;
- não enviar dados sensíveis completos à LLM sem necessidade;
- permitir masking/amostragem;
- log de cada consulta executada pelo agente;
- separação entre geração de SQL e autorização de execução;
- proteção contra instruções maliciosas armazenadas em dados do banco.

---

## Observabilidade e auditoria

Cada conclusão relevante deve responder:

- quem/qual componente produziu;
- quando;
- com quais evidências;
- qual consulta foi executada;
- qual score resultou;
- qual versão do modelo/heurística participou;
- se houve validação humana;
- qual estado anterior foi substituído.

---

## Decisões arquiteturais aprováveis

### ADR-001 — Separar evidência, hipótese e conhecimento

**Decisão:** aprovar.

Motivo: reduz alucinação sem impedir inferência em bases mal modeladas.

### ADR-002 — Descoberta híbrida: heurística + LLM

**Decisão:** aprovar.

Heurísticas determinísticas devem produzir sinais verificáveis; LLM deve ajudar a interpretar e gerar candidatos, não substituir evidência.

### ADR-003 — Knowledge Store persistente e versionado

**Decisão:** aprovar.

O objetivo do projeto exige aprendizado progressivo e reutilização. Recalcular tudo a cada pergunta contraria o próprio produto.

### ADR-004 — SQL de profiling somente leitura por padrão

**Decisão:** aprovar.

A descoberta nunca deve exigir permissão de escrita na base origem.

### ADR-005 — Knowledge Graph conceitual, armazenamento físico desacoplado

**Decisão:** aprovar com ressalva.

O modelo precisa representar grafo de relações, mas isso não obriga usar Neo4j ou outro graph DB no MVP. Pode começar em PostgreSQL com entidades/arestas normalizadas ou JSONB, desde que a abstração preserve o conceito.

---

## O que deliberadamente NÃO decidir agora

- banco definitivo do Knowledge Store;
- vector database definitivo;
- modelo LLM definitivo;
- framework de agentes definitivo;
- event bus;
- Kubernetes;
- microserviços;
- graph database dedicado.

Essas escolhas devem surgir de necessidade comprovada, não de elegância arquitetural.

---

## Resultado da validação do Engineering Agent Stack

### Skills corretamente ativadas

- `architecture` — necessária para decisões estruturais e ADRs.
- `system-design` — necessária para componentes, fronteiras, fluxos e falhas.

### Skills corretamente não ativadas nesta fase

- `frontend-quality` — não há interface em avaliação.
- `deploy-checklist` — ainda não há release.
- `debug` — não há defeito observado.
- `code-review` — ainda não há implementação para revisar.
- `harness` — será usado quando houver critérios executáveis/implementação.

### Próxima skill recomendada

`testing-strategy`, para transformar as hipóteses centrais desta arquitetura em cenários reproduzíveis de teste antes da implementação.
