# La Quinta · Control de despachos

Parcial 1 · Seminario de Actualización · Ingeniería de Sistemas · UNIAJC · 2026-2

Interfaz propia (parte B) que registra despachos de bodega y dispara un escenario de Make (parte C) que valida las existencias antes de producir efectos.

## Qué hace

- **Registrar despacho:** formulario con los seis campos (solicitante, correo, código de producto, cantidad, destino, motivo). Al enviar hace un POST al webhook de Make y muestra la respuesta: aprobado, aprobado con alerta, rechazado o código no válido.
- **Historial de movimientos:** lee la pestaña `movimientos` de la hoja de Google y calcula los dos indicadores del análisis (tiempo de respuesta y despachos bajo el mínimo).

## Configuración

En `index.html`, al comienzo del script, completar:

- `WEBHOOK_URL`: la URL del webhook de Make.
- `SHEET_ID`: el ID de la hoja de Google (el texto entre `/d/` y `/edit`).

La hoja debe estar compartida como «Cualquier persona con el enlace · Lector» y tener las pestañas `inventario`, `movimientos` e `incidentes` (ver `La_Quinta_datos.xlsx`).

## Contrato con Make

Campos que envía la interfaz (formulario codificado): `solicitante`, `correo`, `codigo_producto`, `cantidad`, `destino`, `motivo`, `fecha_hora_solicitud`.

Respuesta que espera (JSON, con el encabezado `Access-Control-Allow-Origin: *`):

```json
{
  "resultado": "APROBADO | APROBADO_ALERTA | RECHAZADO | NO_VALIDO",
  "mensaje": "texto corto",
  "producto": "nombre del producto",
  "saldo_resultante": 38,
  "minimo": 15
}
```

## Publicación

GitHub Pages, desde la rama `main`, carpeta raíz.
