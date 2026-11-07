# Monitor Ambiental — Ingeniería Electrónica

## Contenido
- `index.html`: página web completa (HTML, CSS y JavaScript).
- Usa MQTT sobre WebSockets seguros para recibir datos desde EMQX.
- Incluye tarjetas, gráficas, estados de sensores y detalles técnicos.

## Broker configurado
`wss://broker.emqx.io:8084/mqtt`

El ESP32 puede seguir publicando por MQTT TCP en el puerto 1883. El navegador se conecta por WebSockets seguros.

## Tópicos que escucha la página

| Dato | Tópico |
|---|---|
| Temperatura | `temperatura3/uatf` |
| Humedad | `humedad3/uatf` |
| PPM estimado | `aire3/uatf` |
| Lluvia (%) | `lluvia3/uatf` |
| eCO2 estimado | `eco2/uatf` |
| Índice relativo | `indice/uatf` |
| ADC MQ135 | `adc_mq1353/uatf` |
| Voltaje MQ135 | `voltaje_mq135/uatf` |
| ADC lluvia | `adc_lluvia3/uatf` |

La página también puede escuchar `estado_lluvia/uatf`, pero actualmente calcula una etiqueta visual a partir del porcentaje. El tópico de estado puede incorporarse cuando se defina el formato final del ESP32.

## Importante
- La página ya intenta conectarse al broker al abrirse. Si el ESP32 todavía no publica los tópicos adicionales, esos campos quedarán como `--`.
- Las gráficas muestran las lecturas recibidas mientras la página está abierta; no guardan un historial permanente.
- MQTT público es apropiado para pruebas y demostraciones, no para datos privados ni sistemas de producción.
- La página carga MQTT.js, Chart.js y fuentes desde Internet.

## Probar localmente
Abre `index.html` en un navegador con conexión a Internet. Para una prueba más fiable, también puedes servir la carpeta con un servidor local estático.

## Publicar con GitHub Pages
1. Crea un repositorio nuevo en GitHub.
2. Sube `index.html` a la raíz del repositorio.
3. En Settings → Pages, selecciona la rama principal y la carpeta raíz.
4. Guarda y espera a que GitHub Pages publique la dirección del sitio.

## Próximo paso
Adaptar el programa del ESP32 para publicar todos los tópicos que escucha esta página, manteniendo los pines y el procesamiento de sensores acordados.
