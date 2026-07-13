# FlowGuardian — 4 Decisões Novas (Estratégico v3.1)

**Data:** Julho 2026  
**Contexto:** Validação de Operacional v3.1 e abertura de Estratégico v3.1  
**Status:** Fechado, pronto para implementação em comando  

---

## Decisão 1: MET-10 desdobrado em Período + Total

### Antes
Progressão do épico rastreada só no período de análise.
Exemplo: "Pagamentos: 4 cards movidos em junho"
Limitação: não mostra em que estágio do roadmap o épico realmente tá.

### Depois
Duas métricas complementares, sempre juntas:

**MET-10 Período:** Cards do épico trabalhados no período / Total de cards do épico que aparecem naquele período
- Exemplo: "4 de 17 cards do épico Pagamentos foram trabalhados em junho"
- Signals: Contribuição real do período. Diz quanto você "moveu" do épico naquele mês.

**MET-10 Total:** Cards concluídos do épico / Total de cards do épico (qualquer data)
- Exemplo: "8 de 40 cards do épico Pagamentos estão concluídos no total"
- Signals: Estágio de maturidade. Diz onde o épico tá no roadmap.

### Racional
Velocidade (período) sem destino (total) não comunica risco. Destino sem velocidade não comunica ritmo. Juntas, você vê aceleração (velocidade > ritmo necessário) ou degradação (velocidade < ritmo necessário).

### Impacto no Apêndice Quantitativo
Fórmulas:
```
MET-10 Período = Cards(épico, status=qualquer, data IN [período]) / Cards(épico, data IN [período])
MET-10 Total = Cards(épico, status=CONCLUÍDO) / Cards(épico, data=qualquer)

Sempre reportar ambas. Nunca sumarizar.
```

Coleta:
- Para cada épico, exporte TODOS os cards dele (não filtrado por período)
- O filtro por período entra na fórmula, não na coleta

---

## Decisão 2: MET-10c — Detratores separados (Bloqueados vs Desprioritizados)

### Antes
Detratores de progressão misturados, sem distinção de causa.
Limitação: "épico tá atrasado, teve detratores" não diz se precisa desbloqueio ou se foi deliberado.

### Depois
Dois subtipos explícitos em MET-10c:

**MET-10c Bloqueados:** Cards do épico que começaram trabalho mas ficaram presos em dependência
- N cards, M dias médio de bloqueio (início do bloqueio até resolução)
- Motivo: comentário + flag (D09 cascata)
- Signal: Impedimento. Requer ação de desbloqueio.

**MET-10c Desprioritizados:** Cards do épico que saíram de execução sem conclusão
- P cards (movidos de sprint, cancelados, removidos do épico)
- Motivo: changelog (quem, quando, para onde)
- Signal: Mudança de estratégia. Requer confirmação de intenção.

### Racional
Impedimento e deliberação precisam de recomendações opostas. Reportar junto permite ao Estratégico dar diagnóstico específico (não "épico tá lento", mas "bloqueio de API por 10 dias" ou "3 stories desprioritizadas pra Q3").

### Impacto no Apêndice Quantitativo
Fórmulas:
```
MET-10c Bloqueados = 
  Cards(épico, período) WHERE [flag=bloqueado OR "Aguardando" em comentário]
  Agrupar por: Número de cards, dias médio desde comentário de bloqueio até resolução

MET-10c Desprioritizados = 
  Cards(épico) WHERE [
    (mudança de sprint: FROM sprint(período) TO outra sprint) OR
    (cancelado: transição para CANCELADO durante período) OR
    (removido do épico: mudança de campo Epic durante período)
  ]
  Agrupar por: Número de cards, motivo específico
```

Coleta:
- Changelog de cada card (sprint changes, status changes, epic field changes)
- Comentários (D09 cascata para bloqueios)
- Flag de bloqueio (se disponível)

---

## Decisão 3: Bloqueio Crítico = 10 dias úteis (não 5)

### Antes
Sugestão: bloqueio > 5 dias = crítico
Problema: 5 dias úteis = ~3 semanas de calendário (feriados federais, Carnaval, Corpus Christi contam como úteis em SP). Um card de 2 pontos bloqueado 3 semanas numa iniciativa de 3 meses é ruído. Um de 13 pontos bloqueado 3 semanas numa de 2 semanas é crítico. Dependência de contexto quebra reproducibilidade.

### Depois
Bloqueio > 10 dias úteis = crítico
- 10 dias úteis = ~4 semanas de calendário
- Mais específico: praticamente um ciclo inteiro de sprint sem movimento (sprint é 2 semanas, bloqueio de 2 sprints é escalável)
- Menos falsos positivos que 5

### Racional
Você quer bloquear ruidoso (cards menores, bloqueios curtos) de escalar. 10 dias é um compromisso: curto o suficiente pra não ignorar, longo o suficiente pra não disparar em cada tá-esperando-feedback de 1 semana.

### Impacto no Apêndice Quantitativo
Fórmula:
```
Bloqueio_Critico = bloqueio_dias_uteis > 10
```

Nada muda na estrutura. Só muda o threshold. Reportar:
```
MET-10c Bloqueados Críticos: X cards (> 10 dias úteis)
MET-10c Bloqueados Não-Críticos: Y cards (<= 10 dias úteis)
```

---

## Decisão 4: Risco sem Prazo = Opção B (velocidade vs benchmark)

### Antes
Proposta original: calcular "quantos SPs faltam ÷ velocidade = semanas restantes" se não houver prazo
Problema: "faltam 8 semanas" sem saber quanto era esperado = você não sabe se é lento. Não é risco, é rastreabilidade. Mistura duas métricas pra disparar o mesmo aviso.

### Depois
Opção B: Duas vias distintas de risco

**Com Prazo (obrigatório):**
```
Atraso = Data_Conclusão_Estimada - Data_Prazo_Original
Status = "Em Risco" se Atraso > 0 (qualquer atraso é risco, você decide threshold)
```
Signal: Descolamento de expectativa. Claro.

**Sem Prazo (fallback):**
```
Velocidade_Épico = Cards_Concluídos / Semanas_do_Período
Velocidade_Média_Time = Total_Cards_Concluídos_Período / Semanas_do_Período
Degradação = (Velocidade_Média_Time - Velocidade_Épico) / Velocidade_Média_Time * 100%

Status = "Em Risco" se Degradação > 20% (você decide threshold)
```
Signal: Ritmo abaixo do esperado. Não é estimativa, é degradação observada.

### Racional
O segundo não abandona risco. Usa benchmark de performance real do time (você já calcula Throughput no Operacional) pra detectar se o épico tá lento comparado ao ritmo esperado. "Este épico fez 5 SPs/semana quando o time faz 8 SPs/semana" é risco válido sem precisar de prazo.

### Impacto no Apêndice Quantitativo
Fórmulas:
```
MET-10 Risco (Com Prazo) = 
  Data_Conclusão_Estimada > Data_Prazo_Original
  Atraso em dias
  Status: Verde (no prazo), Laranja (< 5 dias atraso), Vermelho (> 5 dias atraso) [você define thresholds]

MET-10 Risco (Sem Prazo) =
  Velocidade_Épico = Cards_Concluídos(épico) / Semanas
  Velocidade_Time = Throughput_Total(período) / Semanas
  Degradação % = (Velocidade_Time - Velocidade_Épico) / Velocidade_Time * 100%
  Status: Verde (dentro de 10% da média), Laranja (10-20% abaixo), Vermelho (> 20% abaixo) [você define thresholds]
```

Coleta:
- Field "Prazo" do épico (se preenchido)
- Cards concluídos do épico por semana (continuidade da fórmula acima)
- Throughput total do time (já calculado em Operacional, reusar)

---

## Impacto Consolidado no Apêndice Quantitativo do Estratégico

Novas linhas a incluir:

```
MET-10: Progressão de Épicos
├─ MET-10 Período: Cards trabalhados no período / Total de cards do épico (período)
├─ MET-10 Total: Cards concluídos / Total de cards do épico (todo tempo)
├─ MET-10c Bloqueados: N cards, M dias médio (motivo)
├─ MET-10c Desprioritizados: P cards (motivo changelog)
└─ MET-10 Risco: 
    ├─ (Com Prazo) Atraso vs data original
    └─ (Sem Prazo) Degradação vs velocidade média do time (> 20% = risco)
```

Sem mudanças na estrutura de entrada/processo/saída. Só expande o apêndice com fórmulas mais específicas.

---

## Checklist: Pronto pra Estratégico v3.1

- ✓ MET-10 desdobrado (Período + Total, sempre juntos)
- ✓ MET-10c separado (Bloqueados vs Desprioritizados, causas distintas)
- ✓ Threshold de bloqueio crítico (10 dias úteis)
- ✓ Risco sem prazo (Opção B, degradação vs benchmark)
- ✓ Coleta especificada (épicos completos, changelog, velocidade do time)
- ✓ Fórmulas claras (reproducível em qualquer LLM)

Pronto pra implementação.

---

**Data:** Julho 2026  
**Próximo:** Reescrever Comando Estratégico v3.1 com estas 4 decisões embutidas no apêndice
