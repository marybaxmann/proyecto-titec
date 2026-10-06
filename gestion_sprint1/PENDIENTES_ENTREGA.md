# Pendientes — Entrega Evaluación 1

**Cierre:** hoy 01/10 a las 23:59. Lo que se suba después no cuenta.

---

## Listo ✅

- [x] Tabla de responsables por rol en el README.
- [x] INT-01 a INT-08 con responsable y en el tablero.
- [x] HU-04 en In progress con comentario; INT-01, 03, 04 y 07 en In progress.
- [x] README: "79 tests".
- [x] Capturas en `docs/evidencias/capturas/` (estados, error de Auth y base de datos).
- [x] UI3: tokens corregidos en Login y Detalle, ícono de alerta, desviaciones actualizadas.

## Falta ⚠️

- [ ] `frontend/src/components/ui/CampoFormulario.css`, línea 47: cambiar `font-size: font-size: var(--fs-caption);` por `font-size: var(--fs-caption);`.

## En la presentación (no está en capturas)

Mostrar en vivo: acceso denegado (403), formulario con errores (con ícono de alerta) y detalle del evento.

## Preguntas para la llamada con Christopher

- ¿Por qué `_id` y no `id_evento`? → MongoDB obliga a usar `_id`; en la API se muestra como `id_evento`.
- ¿Por qué MongoDB? → ADR-0002.
- ¿Por qué no guardan datos de usuarios? → Son de Auth; Panel solo guarda el id del organizador.

## Para después de la entrega

- [ ] Cuando se haga HU-07 (Sprint 3): actualizar el Swagger de Notificaciones con el formato del contrato v1.3 (INT-06).
