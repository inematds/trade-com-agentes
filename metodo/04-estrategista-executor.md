# 04 — Estrategista e executor

> Paráfrase do vídeo <https://www.youtube.com/watch?v=eg_1NXDcoPk>.

## O que aconteceu

No dia 2, o GPT-6 Astra **parou de executar ordens**. Segundo o autor, o modelo passou a responder
que podia ajudar com a estratégia, mas não iria operar automaticamente em nome dele — e insistir
não mudou nada. Ele tratou como uma restrição do próprio modelo.

## O contorno

A execução saiu do Astra e foi para outro agente:

1. A rotina do Astra termina **mandando um e-mail** com as recomendações.
2. Um **bot executor**, com **e-mail próprio**, tem um **webhook** disparado quando chega mensagem.
3. O bot acorda, lê as recomendações e **manda as ordens para a Alpaca**.
4. O bot também avisa o dono das operações (no dia 5 o autor comenta que acordou com o bot
   mandando as ordens).

Na transcrição automática o bot aparece como "GrokBot" chamado "Trader"; o nome e a plataforma
exata **não foram verificados**.

## Por que isso importa

- **Separar quem pensa de quem executa** acabou sendo forçado, mas é um padrão útil: o estrategista
  não precisa de credencial da corretora, e o executor pode ter regras próprias e simples.
- **O e-mail vira o contrato** entre os dois. Se o formato for livre, o executor tem de interpretar
  texto — e interpretar errado custa dinheiro. Um formato fixo resolve boa parte disso:
  [../templates/recomendacao.json](../templates/recomendacao.json).
- **O que o executor deveria recusar** (nossa sugestão, não está no vídeo): ordem sem stop, ativo fora
  da lista de vigilância, tamanho acima do limite por posição, recomendação velha (com horário
  anterior ao último pregão), e-mail de remetente desconhecido.

## O lado ruim

Contornar a recusa de um modelo com outro agente também tira uma camada de freio. A recusa do
Astra era, na prática, um "tem certeza?" — e o desenho novo removeu essa pergunta.
