PANEL DE MONITOREO AMBIENTAL - 4 ZONAS

Zonas:
1. Zona Central
2. Zona Nueva Terminal
3. Zona Cantumarca
4. Zona Murillo

Compatibilidad con el primer ESP32 (Zona Central):
temperatura3/uatf
humedad3/uatf
aire3/uatf
lluvia3/uatf
eco2/uatf
estado3/uatf

Temas preparados para Zona Nueva Terminal:
uatf/monitoreo/terminal/temperatura
uatf/monitoreo/terminal/humedad
uatf/monitoreo/terminal/aire
uatf/monitoreo/terminal/lluvia
uatf/monitoreo/terminal/eco2
uatf/monitoreo/terminal/estado

Para Cantumarca y Murillo repetir la misma estructura sustituyendo terminal por cantumarca o murillo.

Los tres nuevos ESP32 deben publicar con esos temas exactos para aparecer en la página. El sketch existente del primer ESP32 no fue modificado.
Abrir index.html con Internet. El panel usa MQTT.js y Chart.js desde CDN y se conecta al broker público EMQX por WebSocket seguro.
El historial gráfico vive en memoria mientras la página está abierta. MQ135 PPM/eCO2 son estimaciones; el porcentaje de lluvia es relativo y no representa mm de precipitación.
