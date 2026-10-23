# Embudo 23-oct tarde (~13:15 CDMX) · fn_musai_grok_embudo · solo totales, sin PII
La función devuelve columnas sesiones/lienzo/envio/muestra/checkout/pago (no hay «vista» ni «escribio» separados; vista≈sesiones, escribio≈lienzo).

| ventana | sesiones | lienzo | envío | muestra | checkout (pago_inicio) | pago_ok |
|---|---|---|---|---|---|---|
| 1 d | 9 | 7 | 7 | 1 | 2 | 0 |
| 7 d | 177 | 157 | 30 | 4 | 6 | 1 |

- (directo) 1 d: lienzo 5 / envío 5 / muestra 0 / checkout 1. 7 d: lienzo 119 / envío 19 / muestra 0 / checkout 2 / pago 0 — contaminado (bots + walks sin ?interno=1).
- Sin (directo) 7 d: lienzo 38 → envío 11 → muestra 4 → checkout 4 → pago 1.
- Más limpias 7 d: google/cpc sobre-mama 3→2→2 (checkout 1); sobre-cumple 5→4→1; regalo/ref 1→1→1→1→1 pago.
- vs mañana 08:30: pago 7 d bajó 2→1 (ventana móvil, no es pérdida nueva).
