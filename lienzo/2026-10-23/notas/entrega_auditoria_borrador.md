# BORRADOR · Lienzo · auditoría (entrega viernes 23-oct 18:00 CDMX) · n refresco 23-oct 13:15 CDMX
Para: claude y sam (buzón). Falta: subir capturas/videos a musai-medios/lienzo/2026-10-23/ y poner los enlaces.

## 1 · Qué parte del tráfico es real (solo agregados)
- Corte **23-oct 13:15** (`fn_musai_grok_embudo`): **1 d** sesiones 9 → lienzo 7 → envío 7 → muestra 1 → checkout 2 → pago 0. **7 d** 177 → 157 → 30 → 4 → 6 → 1 (lienzo→pago 0,6 %). Sin (directo) 7 d: 38 → 11 → 4 → 4 → 1. (08:30: 7 d pago 2; bajó por ventana móvil. 14 d 168 → 32 → 5 → 2, corte 08:30.)
- **(directo)** 7 d: lienzo 119 / envío 19 / muestra **0** / pago 0 (1 d: 5 / 5 / 0 / 0) — contaminado. `fn_musai_sesiones_a18` US+(directo) 7 d: operador 1561, bot 141, una_vista 88, prueba 7. Mis walks de Fase 1 y QA Playwright entraron a `/lienzo` **sin** `?interno=1` (avisado a Claude por buzón 23-oct). No proyectar tasas humanas sobre (directo).
- Fuentes más limpias 7 d: google/cpc sobre-mama (3 lienzo → 2 envío → 2 muestra), sobre-cumple (5 → 4 → 1), regalo/ref (1 → 1 → 1 → 1 pago, candidato real).
- 21-oct (histórico): de 106 «(directo)» al lienzo, ~100 bot (1 vista/1 evento, 34 países). Fuga clasificador: `una_vista` exige eventos=0 y el lienzo dispara 1 al cargar. CONFIRMADO en agregados.

## 2 · Las 5 fricciones más caras (por impacto en venta)
1. Muro de cuenta para oír la muestra: tras ~3.5 min (historia, 5 preguntas, estilos, afinar, «Esto entendí»), el único botón es «Entra con Google» o un enlace de correo de 15 px. Visto en iPhone, Android y escritorio (3/3). **23-oct mañana, prod + iPhone automatizado: muro Google 4/4 (CONFIRMADO en ese contexto). Preview, Chrome no headless: MUESTRA sin muro, Google opcional, n=1 (NO confirmado; podría ser diferencia preview/prod o efecto de automatización). Pendiente n=3 390px.** Embudo 30 d: envío 94 -> muestra_vista 26. Competencia (Melodi, Songfinch) pide solo un campo de correo/WhatsApp, sin cuenta.
2. Espera ciega de ~60 s entre la pregunta 5 y los estilos (3/3 equipos), más ~9 s tras «Continuar» y ~20 s en /afinar.
3. Demasiadas decisiones antes de la muestra: afinar se ve obligatorio aunque dice «la receta base ya es perfecta» + confirmación «Esto entendí».
4. Medición rota: ~12 peticiones a musai_visita abortadas y 2 403 por recorrido; bots contados como humanos (punto 1). Sin esto no se puede decidir ningún A/B.
5. España (50/50 con MX): solo USD sin euro, /planes en MXN, ejemplos con mexicanismos (tamales, plática, camión). Ya hay PR #622 con palancas espana_mercado y editor_aviso_aceptar en off, esperando a Claude/Sam. Menores: chips de 40 px y enlaces de 14-15 px (<44 px / <16 px), acotación en inglés en la letra.

## 3 · Tres experimentos (uno a la vez, A/B por último carácter de sesión)
E1 · Medir bien (cola #50, aprobada) — primero, porque sin él no hay n.
- Hipótesis: el embudo humano real es ~5x mejor de lo que parece y hoy no se puede comparar A/B.
- Cambio: el evento automático de carga no cuenta como interacción para una_vista; reintento/keepalive en musai_visita; variante A/B en props.
- Métrica: % de sesiones directo clasificadas bot; visitas abortadas por recorrido = 0.
- n: 7 días. Riesgo: bajo (no toca UI).
E2 · Escuchar la muestra antes de pedir cuenta (cola #49, pendiente de Sam) — la mayor palanca.
- Estado: muro confirmado 4/4 en prod con automatización (mañana 23-oct); en preview no headless se oyó MUESTRA sin Google, n=1. «n=3 @390px (13:27 CDMX): 0/3 muestra; causa CONFIRMADA en preview = POST /api/muestra 403 (fallback sin player ni muro Google). Contraste #118 desktop n=1 = MUESTRA». Si los 3 runs confirman que preview ya deja oír sin cuenta, E2 pasa a ser «llevar a prod / verificar en prod humano» en vez de construir; si no, sigue como está.
- Hipótesis: quitar el muro antes del primer fragmento sube muestra_vista/envío.
- Cambio: reproducir 20-30 s de la muestra sin cuenta; pedir correo (un campo, sin Google obligatorio) para la versión completa/guardarla.
- Métrica: muestra_vista/lienzo_envio y pago_inicio sin bajar.
- n: base ~28 % (26/94); para detectar +15 pp con 80 % de potencia hacen falta ~150 envíos por grupo -> con ~12 envíos humanos/14 d tardaría meses: correr a 7 días mínimo y decidir con n declarado, o empezar con antes/después. Riesgo: toca la promesa «escúchala antes de pagar» (la refuerza) y el flujo de cuenta: va a Sam.
E3 · Feedback en la espera de 60 s.
- Hipótesis: mostrar la historia avanzando (lo que la musa ya entendió, barra con pasos) baja el abandono entre pregunta 5 y estilos.
- Cambio: pantalla de espera con progreso por etapas y una línea de la historia del cliente; sin tocar el motor.
- Métrica: lienzo_envio -> llegada a estilos/afinar (si el evento existe; si no, agregar props).
- n: 100 sesiones humanas por grupo, 7 días mínimo. Riesgo: bajo.

## 4 · Competencia (resumen)
Melodi: ~14 campos obligatorios en el paso 1 (incl. correo y WhatsApp), $599 MXN visible, 10-12 días, sin muestra. Songfinch: correo en el paso 2 de 4 antes de la historia, $179+ USD, sin muestra. Nadie deja oír antes de pagar: es la ventaja de MUSAI y hoy se esconde detrás del muro.
