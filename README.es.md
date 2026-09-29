# Trade con Agentes — el método del desafío de 7 días

**🇧🇷 [Português](README.md) · 🇺🇸 [English](README.en.md) · 🇪🇸 [Español](README.es.md)**

[![Trade con Agentes](guia/assets/banner.jpg)](https://inematds.github.io/trade-com-agentes/guia/es/)

> ## ⚠️ Lee esto primero: este es un texto de estudio, no una recomendación
>
> **No confío en esto para operar.** El trading es de alto riesgo, tiene demasiadas variables y
> **siempre hay alguien del otro lado con información que nosotros no tenemos**. Este repositorio no es
> asesoría financiera, no es una estrategia validada y no es una invitación a poner dinero en un robot.
>
> El objetivo es otro: **aprender de lo que él hizo** — cómo armó los agentes, cómo pasó el
> contexto de uno a otro, dónde se atascó y qué cambió en el camino. El propio resultado del
> desafío lo muestra: en 7 días, el sistema **perdió contra el S&P 500**.

## 📖 Guía de uso

Guía completa (landing + paso a paso): **https://inematds.github.io/trade-com-agentes/guia/es/**

## De dónde viene

Video en YouTube: **"I Gave GPT 6 Astra $10,000 to Trade Stocks...And This Happened"** —
<https://www.youtube.com/watch?v=eg_1NXDcoPk>

El autor le dio US$ 10.000 de dinero real a un agente en **Codex con GPT-6 Astra
(esfuerzo alto)** para operar acciones durante **7 sesiones de bolsa**, con la meta de **superar al S&P 500**. A diferencia de
una prueba anterior suya (con OpenClaw, 30 días, sin tocar nada), aquí podía hacer **hasta dos
cambios por día** — pero no podía apagar el sistema, aunque estuviera perdiendo.

Todo lo que está aquí es **paráfrasis del video**. Los números son **"según lo relatado en el video"**; nada
fue auditado. La transcripción es automática, así que algunos nombres pueden haberse entendido mal (ver
[metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md) (en portugués)).

## El método en una pantalla

```
07:45  premercado    → lee noticias, revisa la cuenta, elige qué vigilar
09:30  1h de sesión  → busca la primera entrada que pase los filtros
11:00  mediodía      → revisa posiciones, última oportunidad de nueva entrada
13:00  tarde         → administra lo que está abierto
14:15  cierre        → cierra las posiciones restantes
14:45  confirmación  → verifica que quedó todo cerrado y registra el resultado del día
15:15  aviso final   → notificación
(horario Central de EE. UU. — sesión de 8:30 a 15:00 CT)

Cada rutina despierta → LEE la nota de handoff de la anterior → actúa → ESCRIBE la próxima nota.
Todas corren en el MISMO hilo: parece un solo agente trabajando todo el día.
```

Desde el día 2 entró una segunda pieza: el modelo **se negó a ejecutar órdenes por sí solo**.
Su solución: Astra pasa a ser solo el **estratega** y termina cada rutina enviando un **correo** con las
recomendaciones a un **bot ejecutor** (que tiene correo propio + webhook). El bot despierta con el
correo y envía la orden al bróker **Alpaca**.

## Contenido

| Archivo | Qué contiene |
|---|---|
| [metodo/01-visao-geral.md](metodo/01-visao-geral.md) (en portugués) | Reglas del desafío, piezas y arquitectura |
| [metodo/02-rotinas.md](metodo/02-rotinas.md) (en portugués) | Las 7 rutinas del día, una por una |
| [metodo/03-handoff.md](metodo/03-handoff.md) (en portugués) | La continuidad: nota de traspaso entre agentes |
| [metodo/04-estrategista-executor.md](metodo/04-estrategista-executor.md) (en portugués) | Por qué separó a quien piensa de quien ejecuta |
| [metodo/05-portoes-de-risco.md](metodo/05-portoes-de-risco.md) (en portugués) | Filtros, relación riesgo/retorno y cómo se aflojaron |
| [metodo/06-diario-7-dias.md](metodo/06-diario-7-dias.md) (en portugués) | Qué pasó cada día (números relatados) |
| [metodo/07-licoes.md](metodo/07-licoes.md) (en portugués) | Qué se puede aprender — y por qué yo no lo copiaría |
| [templates/rotinas.yaml](templates/rotinas.yaml) (en portugués) | Agenda de las rutinas en formato de configuración |
| [templates/handoff.md](templates/handoff.md) (en portugués) | Modelo de la nota de handoff |
| [templates/prompt-rotina.md](templates/prompt-rotina.md) (en portugués) | Modelo de prompt de cada rutina |
| [templates/recomendacao.json](templates/recomendacao.json) (en portugués) | Formato del correo estratega → ejecutor |

**No hay código de operación en este repositorio.** Las plantillas sirven para entender la arquitectura
(o para probar en **cuenta simulada / paper trading**). Si vas a experimentar, empieza por ahí.

## Resultado, según lo relatado

| | Valor final |
|---|---|
| Sistema de agentes | ~US$ 9.900 (≈ −1,0%) |
| Los mismos US$ 10.000 en el S&P 500 | ~US$ 9.980 (≈ −0,2%) |
| Diferencia | el S&P ganó por ≈ 0,8 puntos |

Conclusión del propio autor: 7 sesiones son pocas para decir si la estrategia funciona.

---

Proyecto de estudio de [INEMA.CLUB](https://inema.club) · contenido abierto y gratuito.
