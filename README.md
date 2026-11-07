# Monitoreo Ambiental — Ingeniería Electrónica

## Archivos
- `index.html`: panel web de monitoreo.
- `monitor_ambiental_esp32_mqtt.ino`: programa del ESP32 con sensores y MQTT.

## Broker
- ESP32: `broker.emqx.io`, MQTT TCP, puerto `1883`.
- Navegador: `wss://broker.emqx.io:8084/mqtt`, MQTT sobre WebSockets seguros.

## Tópicos MQTT
| Dato | Tópico |
|---|---|
| Temperatura | `temperatura3/uatf` |
| Humedad | `humedad3/uatf` |
| PPM estimado | `aire3/uatf` |
| Lluvia relativa (%) | `lluvia3/uatf` |
| eCO₂ estimado | `eco2/uatf` |
| Índice relativo | `indice/uatf` |
| ADC MQ135 | `adc_mq1353/uatf` |
| Voltaje MQ135 | `voltaje_mq135/uatf` |
| ADC lluvia | `adc_lluvia3/uatf` |
| Estado lluvia (0 a 4) | `estado_lluvia/uatf` |
| Estado ESP32 (0/1) | `estado3/uatf` |

## Librerías para Arduino IDE
Instalar:
1. `AsyncMqttClient`
2. `AsyncTCP` (dependencia para ESP32)
3. `DHT sensor library` de Adafruit
4. `Adafruit Unified Sensor`

La librería `WiFi.h` viene con el paquete de placas ESP32.

## Antes de cargar el programa
Abre `monitor_ambiental_esp32_mqtt.ino` y reemplaza:
- `TU_NOMBRE_WIFI`
- `TU_CLAVE_WIFI`

No compartas la contraseña de tu Wi-Fi en capturas ni mensajes.

## Calibración pendiente
El programa conserva los parámetros MQ135 `RL = 1.8` y `RO = 32.0` que se indicaron para esta versión. Deben verificarse con el circuito y la calibración real del sensor. Los valores PPM y eCO₂ se muestran como estimaciones del modelo, no como mediciones certificadas.

La lluvia comienza con estas referencias:
- ADC seco: 4095
- ADC mojado: 0

Se deben ajustar después de medir el ADC real con la placa seca y mojada.

## Prueba
1. Selecciona la placa ESP32 correcta y el puerto COM.
2. Abre el Monitor Serial a 115200 baudios.
3. Carga el programa y comprueba que aparezcan `Wi-Fi: CONECTADO` y `MQTT: CONECTADO`.
4. Abre `index.html` en un navegador con Internet.
5. Comprueba que el indicador del servidor MQTT y el estado ESP32 aparezcan conectados.
6. Humedece la placa de lluvia de forma controlada y comprueba que cambie su ADC y porcentaje.

## Publicación web
Puedes alojar `index.html` en GitHub Pages. La página carga MQTT.js y Chart.js desde CDN, por lo que requiere conexión a Internet.

## Limitaciones
- El historial de gráficas es temporal y existe solo mientras la página permanece abierta.
- `broker.emqx.io` es un broker público de pruebas. Los tópicos pueden ser vistos o interferidos por terceros; no usar para información privada ni aplicaciones críticas.


Actualización visual: tablero renovado con tarjeta principal de eCO₂, explicaciones sencillas de cada lectura, resumen de condiciones y una segunda gráfica para las estimaciones del MQ135.
