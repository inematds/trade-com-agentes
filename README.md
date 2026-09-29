# Trade com Agentes — o método do desafio de 7 dias

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

[![Trade com Agentes](guia/assets/banner.jpg)](https://inematds.github.io/trade-com-agentes/guia/)

> ## ⚠️ Leia antes: isto é um texto de estudo, não uma recomendação
>
> **Eu não confio nisso para operar.** Trade é risco alto, tem variáveis demais e **sempre tem
> alguém do outro lado com informação que a gente não tem**. Este repositório não é conselho
> financeiro, não é estratégia validada e não é convite para colocar dinheiro em robô.
>
> O objetivo é outro: **aprender com o que ele fez** — como montou os agentes, como passou o
> contexto de um para o outro, onde travou e o que mudou no caminho. O próprio resultado do
> desafio mostra o ponto: em 7 dias, o sistema **perdeu para o S&P 500**.

## 📖 Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/trade-com-agentes/guia/**

## De onde vem

Vídeo no YouTube: **"I Gave GPT 6 Astra $10,000 to Trade Stocks...And This Happened"** —
<https://www.youtube.com/watch?v=eg_1NXDcoPk>

O autor deu US$ 10.000 de dinheiro de verdade para um agente no **Codex com GPT-6 Astra
(esforço alto)** operar ações por **7 pregões**, com a meta de **bater o S&P 500**. Diferente de
um teste anterior dele (com OpenClaw, 30 dias, sem mexer), aqui ele podia fazer **até duas
mudanças por dia** — mas não podia desligar o sistema, mesmo perdendo.

Tudo que está aqui é **paráfrase do vídeo**. Números são **"conforme relatado no vídeo"**; nada
foi auditado. A transcrição é automática, então alguns nomes podem estar ouvidos errado (ver
[metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md)).

## O método em uma tela

```
07:45  pré-mercado   → lê notícias, confere conta, escolhe o que vigiar
09:30  1h de pregão  → procura a primeira entrada que passe nos filtros
11:00  meio do dia   → revisa posições, última chance de nova entrada
13:00  tarde         → administra o que está aberto
14:15  fechamento    → encerra as posições restantes
14:45  confirmação   → confere se zerou e registra o resultado do dia
15:15  aviso final   → notificação
(horário Central dos EUA — pregão das 8:30 às 15:00 CT)

Cada rotina acorda → LÊ o bilhete de handoff da anterior → age → ESCREVE o próximo bilhete.
Todas rodam na MESMA thread: parece um agente só trabalhando o dia inteiro.
```

A partir do dia 2 entrou uma segunda peça: o modelo **se recusou a executar ordens sozinho**.
Solução dele: o Astra vira só o **estrategista** e termina cada rotina mandando um **e-mail** com as
recomendações para um **bot executor** (que tem e-mail próprio + webhook). O bot acorda com o
e-mail e manda a ordem para a corretora **Alpaca**.

## Conteúdo

| Arquivo | O que tem |
|---|---|
| [metodo/01-visao-geral.md](metodo/01-visao-geral.md) | Regras do desafio, peças e arquitetura |
| [metodo/02-rotinas.md](metodo/02-rotinas.md) | As 7 rotinas do dia, uma a uma |
| [metodo/03-handoff.md](metodo/03-handoff.md) | A continuidade: bilhete de passagem entre agentes |
| [metodo/04-estrategista-executor.md](metodo/04-estrategista-executor.md) | Por que separou quem pensa de quem executa |
| [metodo/05-portoes-de-risco.md](metodo/05-portoes-de-risco.md) | Filtros, relação risco/retorno e como foram afrouxados |
| [metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md) | O que aconteceu em cada dia (números relatados) |
| [metodo/07-licoes.md](metodo/07-licoes.md) | O que dá para aprender — e por que eu não copiaria |
| [templates/rotinas.yaml](templates/rotinas.yaml) | Agenda das rotinas em formato de configuração |
| [templates/handoff.md](templates/handoff.md) | Modelo do bilhete de handoff |
| [templates/prompt-rotina.md](templates/prompt-rotina.md) | Modelo de prompt de cada rotina |
| [templates/recomendacao.json](templates/recomendacao.json) | Formato do e-mail estrategista → executor |

**Não há código de operação neste repositório.** Os templates servem para entender a arquitetura
(ou para testar em **conta simulada / paper trading**). Se for experimentar, comece por aí.

## Resultado, conforme relatado

| | Valor final |
|---|---|
| Sistema de agentes | ~US$ 9.900 (≈ −1,0%) |
| Mesmos US$ 10.000 no S&P 500 | ~US$ 9.980 (≈ −0,2%) |
| Diferença | o S&P venceu por ≈ 0,8 ponto |

Conclusão do próprio autor: 7 pregões é pouco para dizer se a estratégia funciona.

---

Projeto de estudo do [INEMA.CLUB](https://inema.club) · conteúdo aberto e gratuito.
