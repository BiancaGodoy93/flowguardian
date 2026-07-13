# FlowGuardian — Briefing de Continuação
**Data:** 07/07/2026
**Próxima sessão:** Reescrita B (documentação das 19 páginas)

---

## O que foi feito nesta sessão

### 1. Impacto Estratégico v3.1 — Revisado, testado e aprovado

Comando reescrito do zero a partir do v1.0.2. Principais mudanças:

- **Self-contained:** todas as fórmulas, calendário, definições de status e D01–D12 embutidos no comando
- **CT Bruto / Tempo Bloqueado / CT Real:** adicionados como campos obrigatórios (baseline aprovada na sessão anterior com a CE)
- **D10 — Progressão de épico em base dupla:** Base A (período) e Base B (acumulado) sempre juntas, com rótulos fixos
- **"Data estimada de conclusão"** substituindo "Forecast" em todo o comando, com método de cálculo explícito (velocidade × pendentes)
- **Risco com evidência obrigatória:** "Risco: Sim/Não" substituído por exigência de card ou comentário como evidência
- **Card órfão redefinido:** ausência de AMBOS campo Épico e campo Pai (ter só um = vínculo parcial, não órfão)

**Teste:** Sprint 52 fictícia com 10 cards, 3 épicos, 2 iniciativas, 2 bloqueios em comentários, 1 dependência inter-squad crítica, 1 card órfão. Resultado: **16/16 regras CORE atendidas.**

Arquivo: `FLOWGUARDIAN_IMPACTO_ESTRATEGICO_v3.1.md`

---

### 2. Consolidação Executiva — Elevada de v1.1 para v3.1

A CE havia sido aprovada como v1.1 (v1.0.2 + CT Bruto/Bloqueado/Real) nesta mesma sessão, mas sem o tratamento self-contained completo. Antes da consolidação final, foi elevada para v3.1:

- Ganhou os 9 blocos self-contained
- D01–D12 embutidos (subset relevante para síntese)
- Distinção explícita: análise com dados brutos vs. sínteses anteriores
- Todas as proibições e terminologia unificadas com DO e IE

---

### 3. Documento mestre — Consolidação final dos três comandos

Arquivo: `FLOWGUARDIAN_COMANDOS_MASTER_v3.1.md`

Contém os três comandos completos e prontos para copy-paste:

| Comando | Versão | Status |
|---|---|---|
| Diagnóstico Operacional | v3.1 | Aprovado |
| Impacto Estratégico | v3.1 | Aprovado |
| Consolidação Executiva | v3.1 | Aprovado |

Tabela de consistência no final do documento confirma alinhamento entre os três em todos os elementos críticos (CORE-01–07, proibições, CT, D01–D12, terminologia).

---

## Decisões metodológicas ativas (D01–D12)

| Decisão | Descrição |
|---|---|
| D01 | Subtasks excluídas da análise |
| D02 | Cancelados = desperdício ou correção (nunca somados) |
| D03 | "Concluído" conforme status real do board |
| D04 | CT ancora na primeira transição para desenvolvimento ativo |
| D05 | Aging ancora na última transição de status |
| D06–D07 | Calendário: feriados federais + Sexta-feira Santa + 25/jan SP se dia útil |
| D08 | Sprint-mode vs. período-mode detectado automaticamente |
| D09 | Bloqueios: cascata flag → status changelog → comentário |
| D10 | Épicos: Base A (período) + Base B (acumulado) sempre juntas |
| D11 | Escopo: MET-09a/b/c separados, nunca somados |
| D12 | Período-mode: coorte por resolutiondate |

---

## Terminologia proibida (todos os comandos)

| Proibido | Usar no lugar |
|---|---|
| "carry over" | "Planejado (P) × Executado (E)" |
| "Forecast" | "Data estimada de conclusão" |
| "Faróis" / "Níveis de Criticidade" | Status com evidência específica |
| "Risco: Sim" sem evidência | Evidência obrigatória ou "Sem risco documentado" |

---

## Arquivos na pasta Versão Final

| Arquivo | Conteúdo |
|---|---|
| `FLOWGUARDIAN_COMANDOS_MASTER_v3.1.md` | Documento mestre com os três comandos |
| `FLOWGUARDIAN_IMPACTO_ESTRATEGICO_v3.1.md` | Comando IE isolado |

---

## Próximo passo: Reescrita B

Reescrita completa da documentação das 19 páginas (arquitetura já bloqueada).

**Prioridades identificadas no memory do projeto:**
1. Renumerar cross-references nas páginas já migradas (01 e 02) para estrutura atual 00–18
2. Aplicar corte Princípios/CORE a partir da Página 05 (Princípios = filosofia; CORE = regras executáveis)
3. Resolver inconsistência de grafia do nome ("FlowGuardian" vs. "FlowGuardIAn")

**Arquitetura das 19 páginas (bloqueada):**

| Bloco | Páginas |
|---|---|
| Fundamentos | 00 Índice, 01 Visão do Produto, 02 Princípios |
| Concepção da Solução | 03 Arquitetura, 04 Modelo de Dados, 12 Integrações |
| Motor Metodológico | 05 CORE, 06 Prompt Mestre, 07 Casos de Uso, 18 Regras de Inferência |
| Execução e Diagnóstico | 08 Diagnóstico Operacional, 09 Governança Jira, 10 Evidências e Auditoria, 11 Indicadores |
| Governança do Projeto | 13 Premissas e Limitações, 14 Roadmap, 15 Backlog, 16 Registro de Decisões, 17 Glossário |

**Contexto Jira (para referência):**
- Boards: Dev Revenda (4148) e Dev Frota (2726) — projeto B2B
- URL: abasteceai.atlassian.net
- cloudId: `31b09f79-fb9d-4311-91c8-2010d5231d88`

---

## Como retomar

Copie o contexto abaixo para o início da próxima sessão:

```
# FlowGuardian — Continuação da Reescrita B
**Data:** [data de amanhã]

## Status Atual
Os três comandos estão finalizados e aprovados na versão v3.1:
- Diagnóstico Operacional v3.1 ✅
- Impacto Estratégico v3.1 ✅
- Consolidação Executiva v3.1 ✅

Documento mestre consolidado: FLOWGUARDIAN_COMANDOS_MASTER_v3.1.md

## Próximo trabalho
Iniciar a Reescrita B — reescrita completa da documentação das 19 páginas.
Sequenciar página por página, começando pela [indicar por onde quer começar].
Usar os comandos v3.1 como referência canônica para qualquer menção a regras,
métricas ou decisões metodológicas.
```
