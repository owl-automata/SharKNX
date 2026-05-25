# Tipos de Datapoints Compatibles (DPTs)

SharKNX es compatible con los Tipos de Datapoints KNX (Datapoint Types) en dos contextos dentro de su **instalación domótica**:

- **Decodificación (Decoding)** — valores decodificados y mostrados al recibir telegramas en el Monitor. Se aplica a todos los DPTs de este documento para un preciso **diagnóstico KNX**.
- **Envío (Sending)** — DPTs disponibles para su selección al redactar un comando. Un subconjunto de los DPTs decodificables. Marcados con ✅ en la tabla a continuación.

Si llega un telegrama para una dirección de grupo cuyo DPT es desconocido o aún no es compatible, se muestra la carga útil RAW en formato hexadecimal en lugar de un valor decodificado.

---

## Visión general

| DPT | Nombre | Tamaño | Enviar |
|-----|------|------|------|
| **1** | Booleano de 1 bit | 1 bit | ✅ |
| **2** | Controlado de 1 bit | 2 bits | ✅ |
| **3** | Controlado de 3 bits (Paso) | 4 bits | ✅ |
| **4** | Carácter | 1 byte | ✅ |
| **5** | Valor sin signo de 8 bits | 1 byte | ✅ |
| **6** | Valor con signo de 8 bits | 1 byte | ✅ |
| **7** | Valor sin signo de 2 bytes | 2 bytes | ✅ |
| **8** | Valor con signo de 2 bytes | 2 bytes | ✅ |
| **9** | Float de 2 bytes | 2 bytes | ✅ |
| **10** | Hora del día | 3 bytes | ✅ |
| **11** | Fecha | 3 bytes | ✅ |
| **12** | Valor sin signo de 4 bytes | 4 bytes | ✅ |
| **13** | Valor con signo de 4 bytes | 4 bytes | ✅ |
| **14** | Float IEEE 754 de 4 bytes | 4 bytes | ✅ |
| **15** | Acceso de entrada | 4 bytes | — |
| **16** | Cadena de 14 caracteres | 14 bytes | ✅ |
| **17** | Número de escena | 1 byte | ✅ |
| **18** | Control de escena | 1 byte | ✅ |
| **19** | Fecha y hora | 8 bytes | ✅ |
| **20** | Enum de 1 byte | 1 byte | ✅ |
| **21** | Estado / Banderas de 8 bits | 1 byte | ✅ |
| **22** | Estado / Banderas de 16 bits | 2 bytes | ✅ |
| **23** | Conjunto de 2 bits | 1 byte | — |
| **24** | Cadena variable (ISO 8859-1) | variable | — |
| **25** | Doble Nibble | 1 byte | — |
| **26** | Info de escena | 1 byte | — |
| **27** | Info combinada de 32 bits | 4 bytes | — |
| **28** | Cadena variable (UTF-8) | variable | ✅ |
| **29** | Valor con signo de 8 bytes | 8 bytes | ✅ |
| **30** | Activación de canal (24 ch) | 3 bytes | — |
| **206** | Retardo de tiempo + Modo HVAC | 3 bytes | — |
| **217** | Versión | 2 bytes | — |
| **219** | Info de alarma | 6 bytes | — |
| **222** | Consignas de temperatura (×3) | 6 bytes | — |
| **225** | Tiempo de paso de escala | 4 bytes | — |
| **229** | Valor de medición | 6 bytes | — |
| **232** | Color RGB | 3 bytes | ✅ |
| **234** | Código de idioma | 2 bytes | — |
| **235** | Energía activa de tarifa | 6 bytes | — |
| **240** | Posición combinada (persianas) | 3 bytes | — |
| **241** | Estado del actuador de persianas | 4 bytes | — |
| **242** | Color CIE xyY | 6 bytes | ✅ |
| **243** | Transición de color xyY | 8 bytes | — |
| **249** | Transición de brillo y CCT | 6 bytes | ✅ |
| **250** | Control de brillo y CCT (relativo) | 3 bytes | ✅ |
| **251** | Color RGBW | 6 bytes | ✅ |
| **252** | Control relativo RGBW | 5 bytes | ✅ |
| **253** | Control relativo xyY | 4 bytes | — |
| **254** | Control relativo RGB | 3 bytes | ✅ |
| **275** | Cuatro Floats de 2 bytes | 8 bytes | — |

---

## Subtipos

Las siguientes secciones enumeran los subtipos seleccionables al **enviar** comandos (esenciales para el **control KNX**), agrupados por tipo principal. Se omiten los DPTs con un solo subtipo o sin soporte de envío.

### DPT 1 — Booleano de 1 bit

| Subtipo | Descripción |
|---------|-------------|
| 1.001 | Interruptor (Off / On) |
| 1.002 | Booleano |
| 1.003 | Habilitar |
| 1.004 | Rampa |
| 1.005 | Alarma |
| 1.006 | Valor binario |
| 1.007 | Paso |
| 1.008 | Arriba / Abajo |
| 1.009 | Abrir / Cerrar |
| 1.010 | Iniciar / Detener |
| 1.011 | Estado |
| 1.012 | Invertir |
| 1.013 | Estilo de envío de regulación |
| 1.014 | Fuente de entrada |
| 1.015 | Reiniciar |
| 1.016 | Reconocer (Acknowledge) |
| 1.017 | Disparador (Trigger) |
| 1.018 | Ocupación |
| 1.019 | Ventana / Puerta |
| 1.021 | Función lógica |
| 1.022 | Escena A/B |
| 1.023 | Modo de persianas / estores |
| 1.100 | Enfriamiento / Calefacción |

### DPT 2 — Controlado de 1 bit

| Subtipo | Descripción |
|---------|-------------|
| 2.001 | Control de interruptor |
| 2.002 | Control booleano |
| 2.003 | Control de habilitación |
| 2.004 | Control de rampa |
| 2.005 | Control de alarma |
| 2.006 | Control de valor binario |
| 2.007 | Control de paso |
| 2.008 | Control de dirección 1 |
| 2.009 | Control de dirección 2 |
| 2.010 | Control de inicio |
| 2.011 | Control de estado |
| 2.012 | Control de inversión |

### DPT 3 — Controlado de 3 bits

| Subtipo | Descripción |
|---------|-------------|
| 3.007 | Control de regulación (Dimming) |
| 3.008 | Control de persianas |

### DPT 4 — Carácter

| Subtipo | Descripción |
|---------|-------------|
| 4.001 | Carácter (ASCII) |
| 4.002 | Carácter (ISO 8859-1) |

### DPT 5 — Sin signo de 8 bits

| Subtipo | Descripción | Rango | Unidad |
|---------|-------------|-------|------|
| 5.001 | Escala / Porcentaje | 0–100 | % |
| 5.003 | Ángulo | 0–360 | ° |
| 5.004 | Porcentaje | 0–255 | % |
| 5.005 | Proporción | 0–255 | — |
| 5.006 | Tarifa | 0–255 | — |
| 5.010 | Pulsos de contador | 0–255 | — |

### DPT 6 — Con signo de 8 bits

| Subtipo | Descripción | Rango | Unidad |
|---------|-------------|-------|------|
| 6.001 | Porcentaje | −128–127 | % |
| 6.010 | Pulsos de contador | −128–127 | — |

### DPT 7 — Sin signo de 2 bytes

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 7.001 | Pulsos | — |
| 7.002 | Período de tiempo | ms |
| 7.003 | Período de tiempo | 10 ms |
| 7.004 | Período de tiempo | 100 ms |
| 7.005 | Período de tiempo | s |
| 7.006 | Período de tiempo | min |
| 7.007 | Período de tiempo | h |
| 7.011 | Longitud | mm |
| 7.012 | Corriente | mA |
| 7.013 | Brillo | lux |
| 7.600 | Temperatura de color | K |

### DPT 8 — Con signo de 2 bytes

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 8.001 | Diferencia de pulsos | — |
| 8.002 | Retardo de tiempo | ms |
| 8.003 | Retardo de tiempo | 10 ms |
| 8.004 | Retardo de tiempo | 100 ms |
| 8.005 | Retardo de tiempo | s |
| 8.006 | Retardo de tiempo | min |
| 8.007 | Retardo de tiempo | h |
| 8.010 | Diferencia porcentual | % |
| 8.011 | Ángulo de rotación | ° |

### DPT 9 — Float de 2 bytes

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 9.001 | Temperatura | °C |
| 9.002 | Diferencia de temperatura | K |
| 9.003 | Cambio de temperatura | K/h |
| 9.004 | Iluminancia | lux |
| 9.005 | Velocidad del viento | m/s |
| 9.006 | Presión | Pa |
| 9.007 | Humedad | % |
| 9.008 | Calidad del aire (CO₂) | ppm |
| 9.009 | Flujo de aire | m³/h |
| 9.010 | Tiempo | s |
| 9.011 | Tiempo | ms |
| 9.020 | Voltaje | mV |
| 9.021 | Corriente | mA |
| 9.022 | Densidad de potencia | W/m² |
| 9.023 | Kelvin por porcentaje | K/% |
| 9.024 | Potencia | kW |
| 9.025 | Flujo de volumen | l/h |
| 9.026 | Cantidad de lluvia | l/m² |
| 9.027 | Temperatura | °F |
| 9.028 | Velocidad del viento | km/h |

### DPT 13 — Con signo de 4 bytes

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 13.001 | Pulsos de contador | — |
| 13.002 | Tasa de flujo | m³/h |
| 13.010 | Energía activa | Wh |
| 13.011 | Energía aparente | VAh |
| 13.012 | Energía reactiva | VARh |
| 13.013 | Energía activa | kWh |
| 13.014 | Energía aparente | kVAh |
| 13.015 | Energía reactiva | kVARh |
| 13.100 | Retardo de tiempo | s |

### DPT 14 — Float IEEE de 4 bytes (subtipos seleccionados)

Solo un subconjunto de los 80 subtipos del DPT 14 está disponible en la interfaz de usuario de envío. Todos los subtipos se decodifican en el monitor.

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 14.007 | Ángulo | ° |
| 14.019 | Corriente eléctrica | A |
| 14.027 | Potencial eléctrico | V |
| 14.033 | Frecuencia | Hz |
| 14.056 | Potencia | W |
| 14.065 | Velocidad | m/s |
| 14.068 | Temperatura | °C |
| 14.069 | Temperatura absoluta | K |
| 14.070 | Diferencia de temperatura | K |

### DPT 16 — Cadena de 14 caracteres

| Subtipo | Descripción |
|---------|-------------|
| 16.000 | ASCII |
| 16.001 | ISO 8859-1 |

### DPT 20 — Enum de 1 byte

| Subtipo | Descripción |
|---------|-------------|
| 20.002 | Modo de edificio |
| 20.003 | Modo de ocupación |
| 20.004 | Prioridad |
| 20.005 | Modo de aplicación de luz |
| 20.006 | Área de aplicación de luz |
| 20.007 | Tipo de clase de alarma |
| 20.008 | Modo PSU |
| 20.013 | Retardo de tiempo |
| 20.014 | Fuerza del viento (Beaufort) |
| 20.100 | Tipo de combustible |
| 20.101 | Tipo de quemador |
| 20.102 | Modo HVAC |
| 20.103 | Modo DHW (ACS) |
| 20.104 | Prioridad de carga |
| 20.105 | Modo de control HVAC |
| 20.106 | Modo de emergencia HVAC |
| 20.107 | Modo de conmutación (Changeover) |
| 20.108 | Modo de válvula |
| 20.109 | Modo de compuerta |
| 20.110 | Modo de calentador |
| 20.111 | Modo de ventilador |
| 20.112 | Modo Maestro / Esclavo |
| 20.113 | Estado de consigna de habitación |

> **Nota:** La visualización de las etiquetas enum para la mayoría de los subtipos DPT 20 vuelve a utilizar el número de modo RAW de forma predeterminada. Las etiquetas con nombre (por ejemplo, "Confort", "Standby") se muestran para el 20.102 (Modo HVAC) y algunos otros en su panel de control de **edificios inteligentes**.

### DPT 21 — Banderas de estado de 8 bits

| Subtipo | Descripción |
|---------|-------------|
| 21.001 | Estado general |
| 21.002 | Control de dispositivo |
| 21.100 | Señal de forzado |
| 21.102 | Estado del controlador de calefacción de habitación |
| 21.103 | Estado del controlador solar DHW |
| 21.105 | Estado del controlador de enfriamiento de habitación |
| 21.106 | Estado del controlador de ventilación |

### DPT 22 — Banderas de estado de 16 bits

| Subtipo | Descripción |
|---------|-------------|
| 22.100 | Estado del controlador DHW |
| 22.101 | Estado RHCC |

### DPT 29 — Con signo de 8 bytes (Energía de 64 bits)

| Subtipo | Descripción | Unidad |
|---------|-------------|------|
| 29.010 | Energía activa | Wh |
| 29.011 | Energía aparente | VAh |
| 29.012 | Energía reactiva | VARh |

### DPT 232 / 242 / 249 / 250 / 251 / 252 / 254 — Color e Iluminación

| DPT | Descripción | Tamaño |
|-----|-------------|------|
| 232.600 | Color RGB | 3 bytes |
| 242.600 | Color CIE xyY | 6 bytes |
| 249.600 | Transición de brillo y temperatura de color | 6 bytes |
| 250.600 | Control de brillo y temperatura de color (relativo) | 3 bytes |
| 251.600 | Color RGBW | 6 bytes |
| 252.600 | Control relativo RGBW | 5 bytes |
| 254.600 | Control relativo RGB | 3 bytes |

---

## DPTs de solo decodificación

Los siguientes DPTs se decodifican en el monitor cuando el proyecto **ETS** proporciona la asignación del DPT, pero no están disponibles para la composición manual de comandos en la interfaz de usuario de envío.

| DPT | Descripción |
|-----|-------------|
| 15.000 | Acceso de entrada (código de acceso) |
| 23.x | Conjunto de acciones de 2 bits (on/off, up/down, alarm) |
| 24.x | Cadena de longitud variable (ISO 8859-1) |
| 25.x | Doble Nibble |
| 26.001 | Info de escena |
| 27.001 | Info combinada de bits On/Off |
| 30.1010 | Activación de canal (24 canales) |
| 206.x | Retardo de tiempo + Modo HVAC/DHW/Ocupación/Edificio |
| 217.001 | Versión DPT |
| 219.001 | Info de alarma |
| 222.x | Consignas de temperatura de habitación (×3) |
| 225.x | Tiempo de paso de escala |
| 229.001 | Valor de medición |
| 234.001 | Código de idioma (ISO 639-1) |
| 235.001 | Energía activa de tarifa |
| 240.800 | Posición combinada (persianas/estores) |
| 241.800 | Estado del actuador de persianas |
| 243.x | Transición de color xyY |
| 253.x | Control relativo xyY |
| 275.x | Cuatro Floats de 2 bytes |
