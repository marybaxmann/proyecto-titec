# Política de autorización — textos para pegar en cada HU

Pegar al final de la descripción de cada issue, después de los criterios de aceptación.

---

## Bloque común (va en todas las HU con usuario)

```markdown
### Política de autorización
- La sesión se valida con Auth en cada petición (`GET /internal/validar-sesion`), reenviando la cookie `jwt` sin modificarla.
- La identidad es el `id_usuario` retornado por Auth; nunca un id enviado por el Frontend.
- Sesión inválida o expirada → `401` y redirección al login.
- Auth no disponible → `503` (Fail-Secure).

### Definition of Done
Ver [DEFINITION_OF_DONE.md](https://github.com/marybaxmann/Equipo-1---Panel-Organizador/blob/main/docs/DEFINITION_OF_DONE.md).
```

---

## Regla específica por HU (agregar debajo del bloque común)

### HU-01 — Crear un evento
```markdown
- Solo el rol `organizador` puede crear eventos; otro rol → `403`.
- El evento se asocia al `id_usuario` retornado por Auth como propietario.
```

### HU-02 — Editar un evento
```markdown
- Solo el rol `organizador` puede editar; otro rol → `403`.
- Solo el propietario del evento puede editarlo; si no es el propietario → `403`.
- Evento inexistente → `404`.
```

### HU-03 — Eliminar un evento
```markdown
- Solo el rol `organizador` puede eliminar; otro rol → `403`.
- Solo el propietario del evento puede eliminarlo; si no es el propietario → `403`.
- Evento inexistente → `404`.
```

### HU-04 — Publicar un evento
```markdown
- Solo el rol `organizador` puede publicar; otro rol → `403`.
- Solo el propietario del evento puede publicarlo; si no es el propietario → `403`.
- Evento inexistente → `404`.
```

### HU-05 — Ver mis eventos
```markdown
- Solo el rol `organizador` accede a la vista administrativa; otro rol → `403`.
- Se listan únicamente los eventos cuyo propietario es el `id_usuario` retornado por Auth.
```

### HU-06 — Verificación de autorización del organizador
```markdown
- Esta HU implementa la política común para todas las HU: validación con Auth, rol `organizador` para acciones administrativas y validación de propiedad del evento.
- Lectura de un evento por otros microservicios (`GET /api/v1/panel/eventos/{id_evento}`): roles `staff` y `organizador`, según contrato con Check-in.
```

### HU-07 — Notificar cambios de estado (sin bloque común)
```markdown
### Política de autorización
- No expone endpoints al Frontend: la publicación al broker se ejecuta solo después de una operación ya autorizada (HU-02, HU-03 o HU-04).
- Los mensajes del broker no incluyen la cookie de sesión ni datos personales del organizador.

### Definition of Done
Ver [DEFINITION_OF_DONE.md](https://github.com/marybaxmann/Equipo-1---Panel-Organizador/blob/main/docs/DEFINITION_OF_DONE.md).
```
