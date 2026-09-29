# 01 — Visão geral

> Paráfrase do vídeo <https://www.youtube.com/watch?v=eg_1NXDcoPk>. Estudo, não recomendação.

## As regras do desafio

- **Capital:** US$ 10.000 de dinheiro real, numa conta de corretora.
- **Prazo:** 7 pregões (começou numa quarta-feira, 9 de setembro, segundo o autor).
- **Meta:** terminar à frente do **S&P 500** no mesmo período — não "ficar rico". Se o S&P cair 10%
  e o sistema cair 5%, conta como vitória.
- **Intervenção:** até **duas mudanças por dia** no sistema. Não pode desligar, mesmo perdendo tudo.
- **Só ações.** Sem opções nem alavancagem (o autor diz que opções mudariam o jogo para os dois lados).
- **Aposta pública:** se perdesse para o S&P, daria um ingresso VIP de um evento dele para a audiência.

## As peças

| Peça | Papel |
|---|---|
| **Codex + GPT-6 Astra (esforço alto)** | Cérebro: pesquisa, notícias, escolha de ativos, decisão de entrada e saída |
| **Subagentes de pesquisa** | Na montagem, o Astra delegou pesquisa a vários "agentes de trading" para desenhar a estratégia |
| **Rotinas agendadas** | 7 despertares por pregão, cada um com uma tarefa (ver [02-rotinas.md](02-rotinas.md)) |
| **Handoff** | Bilhete que cada rotina deixa para a próxima (ver [03-handoff.md](03-handoff.md)) |
| **Uma thread só** | Todas as rotinas rodam na mesma conversa — dá para acompanhar o dia inteiro num lugar |
| **Bot executor** (a partir do dia 2) | Recebe as recomendações por e-mail e manda as ordens (ver [04-estrategista-executor.md](04-estrategista-executor.md)) |
| **Alpaca** | Corretora com API, onde as ordens são executadas |

## Como a estratégia nasceu

O autor não chegou com uma estratégia pronta. Ele descreveu o desafio ao agente (capital, prazo, meta)
e pediu muita pesquisa. O agente distribuiu o trabalho entre subagentes e voltou com um plano:
operações de curto prazo dentro do dia, com filtros de entrada, stop e relação risco/retorno mínima
de **2 para 1**, zerando tudo antes do fechamento.

## Arquitetura (depois do dia 2)

```
          ┌──────────────────── mesma thread no Codex ────────────────────┐
agenda →  │ rotina N: lê handoff → notícias/conta → decide → escreve handoff │
          └───────────────┬────────────────────────────────────────────────┘
                          │ e-mail com recomendações
                          ▼
                 bot executor (e-mail próprio + webhook)
                          │ ordem
                          ▼
                       Alpaca  → posição / stop / venda
```

## O que muda ao longo da semana

O desenho original era **conservador**: poucas entradas, filtros duros, zerar no fim do dia. Nos
primeiros dias quase nada aconteceu, e o autor foi **afrouxando** — mais revisões de entrada, relação
risco/retorno menor, menos portões e, depois, posições carregadas de um dia para o outro. Essa
progressão é a parte mais instrutiva do vídeo (ver [05-portoes-de-risco.md](05-portoes-de-risco.md)
e [07-licoes.md](07-licoes.md)).
