# 02 — As rotinas do dia

> Paráfrase do vídeo <https://www.youtube.com/watch?v=eg_1NXDcoPk>. Horários em **Central Time (CT)**;
> o pregão americano vai das 8:30 às 15:00 CT (9:30 às 16:00 em Nova York).

O autor fala em "seis despertares de ação e dois de notificação", mas lista **sete horários**. A
lista abaixo segue os horários mostrados. Na véspera do dia 1 as rotinas aparecem desativadas: só
ligam quando há pregão.

| Horário (CT) | Rotina | O que faz |
|---|---|---|
| 07:45 | **Pré-mercado** | Lê notícias, confere a conta, escolhe a lista de ações para vigiar no dia |
| 09:30 | **Primeira entrada** | Cerca de 1h depois da abertura, procura a primeira operação que passe nos filtros |
| 11:00 | **Meio do dia** | Revisa as posições e considera a **última** entrada nova do dia |
| 13:00 | **Tarde** | Administra o que está aberto (stop, alvo, saída) |
| 14:15 | **Fechamento** | Encerra as posições que sobraram |
| 14:45 | **Confirmação** | Confere se a conta ficou zerada e registra o resultado do dia |
| 15:15 | **Aviso** | Notificação final (depois do fechamento) |

## Como as rotinas mudaram

| Quando | Mudança pedida pelo autor |
|---|---|
| Fim do dia 1 | "Plano mais ativo": **três** revisões de entrada, filtros menos restritivos, risco/retorno mínimo de 2:1 → **1,5:1** |
| Fim do dia 2 | Quer o agente acordando **mais vezes** (fala em "a cada 30 minutos") e com **menos portões** — as boas ideias eram barradas no último filtro |
| Dia 3 → 4 | Pede para usar mais do caixa (60% estava parado). A partir daí aparecem posições **carregadas de um dia para o outro**, o que contraria o "zerar até 14:15" original |

A agenda como configuração está em [../templates/rotinas.yaml](../templates/rotinas.yaml), e o
modelo de prompt de cada rotina em [../templates/prompt-rotina.md](../templates/prompt-rotina.md).

## Por que tantas rotinas e não um agente ligado o dia todo

- Cada despertar tem **uma pergunta só** (o que vigiar? entro? saio? zerei?). Isso reduz o espaço
  para o modelo "inventar moda".
- Rodar em horários fixos deixa o custo previsível e o histórico fácil de auditar.
- O risco é o oposto: entre um despertar e outro **ninguém está olhando**. A proteção nesse
  intervalo é a ordem de stop na corretora — e no dia 1 foi justamente o stop que disparou na hora.
