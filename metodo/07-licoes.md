# 07 — Lições (e por que eu não copiaria)

> Opinião do INEMA sobre o vídeo <https://www.youtube.com/watch?v=eg_1NXDcoPk>. Estudo, não
> recomendação.

## Por que eu não confio nisso para operar

- **Trade é risco alto.** O dinheiro some mais rápido do que aparece, e o agente não sente a perda.
- **Variáveis demais.** Juros, notícia, humor do mercado, liquidez, horário — no dia 6 uma decisão
  do Fed desfez o trabalho da semana em uma hora.
- **Sempre tem alguém com informação que a gente não tem.** Do outro lado da ordem estão fundos,
  mesas e algoritmos com dados, velocidade e capital muito maiores. Um agente lendo notícia pública
  às 7:45 chega depois.
- **Sete dias é ruído.** O próprio autor diz isso. Nenhum resultado nesse prazo — positivo ou
  negativo — prova coisa alguma.

## O que vale aprender (e serve para outros agentes)

1. **Rotinas curtas com uma pergunta cada** são mais fáceis de controlar e auditar do que um agente
   ligado o dia inteiro.
2. **Handoff escrito** resolve a falta de memória entre execuções — desde que o estado "duro"
   (saldo, posições) venha da fonte oficial, não do bilhete.
3. **Uma thread só** dá ao dono uma visão contínua do que aconteceu. Observabilidade barata.
4. **Separar estrategista e executor** com um contrato de mensagem fixo é um bom padrão — o executor
   pode ter regras simples e duras de recusa.
5. **Meta relativa (bater o índice)** é mais honesta do que meta absoluta ("ganhar X").

## O que o experimento mostrou sem querer

- **Portões apertados → nada acontece.** Portões frouxos → muita coisa acontece, e pior que o índice.
  O "botão" que o dono girou foi o de risco, não o de qualidade.
- **Pressão de prazo e de plateia** fez o humano pedir mais agressividade. O agente obedeceu. O
  elo fraco não era o modelo.
- **A recusa do modelo foi contornada**, e junto foi embora um freio.
- **Regras que mudam todo dia** impedem saber o que funcionou: cada dia foi um sistema diferente.
- **Zerar no fim do dia virou carregar posição**, e foi justamente no pernoite que vieram as quedas
  (abertura do dia 4) e no evento macro (dia 6).

## Se for estudar na prática

- Use **conta simulada (paper trading)** — a Alpaca oferece uma.
- Defina as regras **antes** e não mude durante o período de teste.
- Registre cada decisão com a tese e compare com o índice no **mesmo** período.
- Rode por meses, não dias, antes de tirar qualquer conclusão.
- Coloque limites no executor que o estrategista não consegue desligar (tamanho máximo, stop
  obrigatório, perda máxima diária).
