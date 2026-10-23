# Clima de la mañana (n8n)

Workflow de [n8n](https://n8n.io) que cada día a las 7:00 (hora de Lima) consulta el clima de Piura y lo envía por correo.

```
[Cada mañana a las 7] → [Mi ciudad] → [Buscar coordenadas] → [Obtener clima] → [Resumen del clima] → [Enviar por Gmail]
```

## Qué hace cada nodo

| Nodo | Tipo | Función |
|---|---|---|
| Cada mañana a las 7 | Schedule Trigger | Inicia el workflow todos los días a las 7:00. |
| Mi ciudad | Edit Fields | Define la ciudad (`Piura`). Cámbiala aquí para usar otra. |
| Buscar coordenadas | HTTP Request | Convierte el nombre de la ciudad en latitud y longitud con la API de geocodificación de Open-Meteo. |
| Obtener clima | HTTP Request | Pide a Open-Meteo la temperatura actual, la sensación térmica, el viento, la máxima, la mínima y la probabilidad de lluvia del día. |
| Resumen del clima | Edit Fields | Extrae los datos útiles y arma un mensaje legible. |
| Enviar por Gmail | Send Email (SMTP) | Envía el mensaje por correo. |

Usa [Open-Meteo](https://open-meteo.com), que es gratuito y no necesita API key.

## Cómo usarlo

1. En n8n, crea un workflow nuevo y elige **⋯ → Import from File** → `clima-de-la-manana.json`.
2. En el nodo **Enviar por Gmail**, crea una credencial SMTP:
   - Host `smtp.gmail.com`, puerto `465`, SSL/TLS activado.
   - Usuario: tu Gmail. Contraseña: una [contraseña de aplicación](https://myaccount.google.com/apppasswords) (requiere la verificación en 2 pasos).
3. Cambia el remitente y el destinatario del correo por los tuyos.
4. Pulsa **Execute workflow** para probarlo y actívalo para que se ejecute cada día.

Ejemplo del mensaje:

> Buenos días. En Piura hace 25.6°C (sensación 29°C). Hoy: mín 23.7°C, máx 29.3°C, 75% de probabilidad de lluvia.
