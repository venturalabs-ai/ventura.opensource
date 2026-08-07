# Skill: ventura.opensource — LOOP Skill Engine / Deterministic Replay

Skill de estudo com materiais gratuitos (livros e guias) usando **execução
determinística**: explore a trilha uma vez, compile o plano de leitura,
replique a leitura diária com ~zero tokens, regenere quando o objetivo mudar.

## Trigger

Use quando o usuário quiser: estudar por livros gratuitos, montar plano de
leitura, "o que ler hoje", escolher material sobre um tópico, revisar
conteúdo estudado.

## Arquitetura Token-Efficient & Regenerative

| Fase | Descrição | Consumo |
|---|---|---|
| **Explore** | Modelo forte analisa trilha + objetivo (uma vez) | Alto (único) |
| **Compile** | Gera `leitura.md`: capítulos, metas, prazo, resumo | Baixo |
| **Replay** | Leitura do dia — capítulo, resumo, exercício | Mínimo/Zero |
| **Regenerate** | Trilha/objetivo mudou → regenere o plano | Sob demanda |

## Receita determinística (Replay)

```text
1. PEDIDO   — "leitura de hoje" | "próximo capítulo" | "revisar trilha"
2. RECEITA  — consulta leitura.md: capítulo N, resumo, exercício, meta
3. EXECUTA  — 1. lê o capítulo | 2. registra resumo de 5 linhas
             3. faz 1 exercício prático
4. REGISTRA — progresso, dificuldade, dúvidas, data
5. STOP-YIELD — material sem valor/desatualizado → propõe troca
```

## Regras de engenharia

- **Token Budget** — Explore: até 6k tokens. Replay: < 200 tokens.
- **Context Firewall** — o replay só vê a leitura do dia (nunca o plano inteiro).
- **Prefix Caching** — o sistema deste arquivo fica byte-stable.
- **Skill Distillation** — trilha validada vira plano permanente.
- **Regeneração** — novo tópico/meta → volta ao Explore com memória.

## Como compilar o plano (Explore → Compile)

```text
1. Entrevista rápida: tópico, nível, tempo semanal, objetivo
2. Seleciona a trilha curada e o material gratuito mais adequado
3. Compila leitura.md: capítulos, metas semanais, resumo, exercícios
4. Valida com o usuário e ativa o Replay
```

## Exemplo de uso

```text
Atue como ventura.opensource (modo REPLAY). Meu leitura.md diz: "Python,
Capítulo 4: estruturas de dados". Liste o resumo esperado, o exercício
prático e a meta de tempo para hoje. Use menos de 200 tokens e registre o
progresso.
```
