# 03 — Handoff: a continuidade entre agentes

> Paráfrase do vídeo <https://www.youtube.com/watch?v=eg_1NXDcoPk>.

## O problema

Cada rotina é um agente que acorda do zero. Sem memória, ele não sabe por que comprou aquela ação,
qual era o stop, o que já foi tentado ou o que o dono pediu ontem. O autor queria evitar agentes
"sem estado e inúteis".

## A solução dele

1. **Todo agente, antes de terminar, escreve um bilhete de handoff** para o próximo.
2. **Todo agente, ao acordar, lê o último bilhete** antes de fazer qualquer coisa.
3. **Todas as rotinas rodam na mesma thread.** O histórico fica num lugar só, então o resultado
   parece um único agente trabalhando o dia inteiro — e o dono acompanha tudo numa tela.

## O que um bom bilhete precisa ter

O vídeo não mostra o texto dos bilhetes. O modelo abaixo é **nossa reconstrução** do que a
continuidade exige, com base no que cada rotina precisa saber:

- **Estado da conta:** caixa, patrimônio, posições (ativo, quantidade, preço médio, stop, alvo).
- **Tese de cada posição:** por que entrou e o que invalida a ideia.
- **Lista de vigilância** do dia e o motivo de cada nome.
- **O que foi rejeitado e por quê** (evita reanalisar a mesma coisa a cada rotina).
- **Pedidos do dono ainda válidos** ("seja mais ativo", "use o caixa parado").
- **Próxima ação esperada** da rotina seguinte.
- **Ordens enviadas ao executor** e a confirmação (ou não) de que foram executadas.

Modelo pronto: [../templates/handoff.md](../templates/handoff.md).

## Ponto de atenção

O bilhete é **texto escrito pelo próprio modelo**. Se uma rotina registrar um preço ou uma posição
errada, a próxima herda o erro. Por isso o estado da conta deve vir **da corretora** a cada
despertar, e o bilhete serve para a parte que a corretora não guarda: a intenção, a tese e o plano.
