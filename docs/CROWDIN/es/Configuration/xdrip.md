# Configuración de xDrip+

Si todavía no lo has hecho, descarga [xDrip+](https://github.com/NightscoutFoundation/xDrip)

Para los transmisores G6 fabricados después de otoño/finales de 2018 (es decir, con números de serie que empiezan por 80 u 81) por favor, asegúrate de utilizar la versión [maestra fechada 2019/05/18 ](https://jamorham.github.io/#xdrip-plus) o posterior.

Si el número de serie de su transmisor Dexcom G6 empieza por 8G u 8H utiliza una de las [últimas compilaciones nocturnas](https://github.com/NightscoutFoundation/xDrip/releases).

## Configuración básica para todos los medidores contínuos (CGM), sistemas CGM puros o sistemas flash (FGM)

* Asegúrate de establecer la URL base correctamente utilizando **https://** y no http://
   
   Por ejemplo, https://TU_API_SECRET@nombre_de_tu_app.herokuapp.com/api/v1/
   
   -> Pulsa en la hamburguesa (menú con tres líneas de la parte superior izquierda de la pantalla) -> Configuración-> Subir a la nube-> Sincronización con Nightscout (REST-API) -> URL base

* Desactiva `Calibración automática` Si la caja de verificación `Automatic Calibration` está marcada, activa `Descargar datos` y a continuación desmarca la caja de verificación de `Calibración automática` y desactiva `Descargar datos` de nuevo, de lo contrario los tratamientos (insulina y carbohidratos) se añadirán dos veces a Nightscout.

* Pulsa `Opciones adicionales`

* Desactiva `Cargar tratamientos` y `Rellenar datos`.
   
   **Advertencia de seguridad: Debes desactivar "Cargar tratamientos" en xDrip+, de lo contrario, si los tratamientos se duplican pueden dar lugar a cifras erróneas de insulina activa (IOB) y carbohidratos activos (COB) en en AAPS.**

* La opción `Alerta de fallos` también debe desactivarse. De lo contrario, recibirás una alarma cada 5 minutos si la red wifi/móvil es demasiado mala o si el servidor no está disponible.
   
   ![xDrip+ Ajustes Básicos 1](../images/xDrip_Basic1.png)
   
   ![xDrip+ Ajustes Básicos 2](../images/xDrip_Basic2.png)

* **Configuración InterApps** Si vas a utilizar AndroidAPS es necesario activar <0>Difusión local</0> dentro de las opciones InterApps de xDrip+ para que los datos sean emitidos y AndroidAPS pueda leerlos.

* Para que los valores sean consistentes, debes activar `Enviar el valor de glucosa visualizado`.

* Si has activado `Aceptar tratamientos` en xDrip+ y <0>Difusión de datos</0> en AndroidAPS, entonces xDrip+ recibirá los datos de insulina, carbohidratos y dosis basal desde AndroidAPS para poder realizar predicciones de hipoglucemia, etc. con mayor precisión.
   
   ![xDrip+ Ajustes Básicos 3](../images/xDrip_Basic3.png)

### Identificar receptor

* Si descubres problemas con la difusión local (AAPS no recibe los valores de glucemia en sangre (BG) de xDrip+) ve a Ajustes > Ajustes InterApp > Identificar receptor y especifica `info.nightscout.androidaps`.
* Importante: la corrección automática a veces tiende a cambiar la "i" de "info" por una mayúscula. Debes utilizar **solo letras minúsculas** al escribir `info.nightscout.androidaps`. Las mayúsculas impedirían que AAPS recibiera valores de glucemia en sangre (BG) desde xDrip+.
   
   ![xDrip+ Inter-app Ajustes Básicos Identificar receptor](../images/xDrip_InterApp_NS.png)

## xDrip+ & Dexcom G6

* El transmisor Dexcom G6 puede conectarse simultáneamente al receptor Dexcom (o alternativamente a la bomba t:slim) y a una aplicación en tu teléfono.
* Para usar xDrip+ como receptor, desinstala primero la aplicación Dexcom. **No se puede conectar al mismo tiempo la aplicación xDrip+ y Dexcom con el transmisor.**
* Si necesitas utilizar Clarity (app Dexcom) y quieres beneficiarte de las alarmas de xDrip+ utiliza la [aplicación Dexcom parcheada](../Hardware/DexcomG6#if-using-g6-with-patched-dexcom-app) y la opción de difusión local a xDrip+.

### La versión de xDrip+ a utilizar depende del número de serie de los transmisores G6.

* Para los transmisores G6 fabricados después de otoño/finales de 2018 (es decir, con números de serie que empiezan por 80 u 81) por favor, asegúrate de utilizar la versión [maestra fechada 2019/05/18 ](https://jamorham.github.io/#xdrip-plus) o posterior. 
* Si el número de serie de su transmisor Dexcom G6 Si el número de serie de su transmisor Dexcom G6 empieza por 8G u 8H utiliza una de las últimas [compilaciones nocturnas con fecha 2019/07/28 o posterior](https://github.com/NightscoutFoundation/xDrip/releases).

### Ajustes específicos de Dexcom

* Abra G5/G6 Configuración de depuración -> Menú Hamburguesa (parte superior izquierda de la pantalla de inicio) -> Settings -> G5/G6 Debug Settings ![Abrir los ajustes de xDrip+](../images/xDrip_Dexcom_SettingsCall.png)

* Habilite los siguientes parámetros
   
   * `Usar el Colector OB1`
   * `Algoritmo nativo` (importante si desea utilizar SMB)
   * `Soporte G6`
   * `Permitir desvinculación de OB1`
   * `Permitir a OB1 iniciar la vinculación`
* Todas las demás opciones deben ser desactivados
* Ajuste el nivel de aviso de la batería a 280 (parte inferior de los valores de depuración G5/G6)
   
   ![ajustes de depuración de xDrip+ G5/G6](../images/xDrip_Dexcom_DebugSettings.png)

### No se recomiendan reinicios preventivos

**Con transmisores Dexcom con número de serie que empieza por 8G o 8H, los reinicios preventivos no funcionan y podrían matar el sensor completamente!**

No se recomienda la extensión automática de los sensores Dexcom (`reinicios preventivos`) ya que esto podría conducir a "saltos" en los valores BG el día 9 después del reinicio.

![xDrip+ Saltar después de un reinicio preventivo](../images/xDrip_Dexcom_PreemptiveJump.png)

Lo que está claro es que el uso del G6 es tal vez un poco más complejo que lo que se sugiere en primer lugar. Para utilizar de manera segura, hay un par de puntos a tener en cuenta:

* Si estás usando los datos nativos con el código de calibración en xDrip+ o Spike, la cosa más segura es no permitir reinicios preventivos del sensor.
* Si debe usar reinicio preventivo, a continuación, asegúrese de insertar una hora del día donde puede observar el cambio y calibrar si es necesario. 
* Si está reiniciando sensores, o bien haga esto sin la calibración de fábrica para obtener resultados más seguros en los días 11 y 12, o asegúrate de que estás listo para calibrar y vigilar la variación.
* La preabsorción del G6 con calibración de fábrica es probable que dé variaciones en los resultados. Si haces preconfiguración, entonces para obtener los mejores resultados, probablemente necesitarás calibrar el sensor.
* Si no estás observando los cambios que pueden estar teniendo lugar, puede ser mejor volver al modo no calibrado en fábrica y usar el sistema como un G5.

Para obtener más información acerca de los detalles y las razones de estas recomendaciones, lea el [artículo completo](http://www.diabettech.com/artificial-pancreas/diy-looping-and-cgm/) publicado por Tim Street en [www.diabettech.com](http://www.diabettech.com).

### Conectar el transmisor G6 por primera vez

**Para el segundo y los siguientes transmisores ver [Extender la vida del transmisor](../Configuration/xdrip#extend-transmitter-life) a continuación.**

Para los transmisores G6 fabricados después de otoño/finales de 2018 (es decir, con números de serie que empiezan por 80 u 81) por favor, asegúrate de utilizar la versión [maestra fechada 2019/05/18 ](https://jamorham.github.io/#xdrip-plus) o posterior.

Si el número de serie de su transmisor Dexcom G6 Si el número de serie de su transmisor Dexcom G6 empieza por 8G u 8H utiliza una de las últimas [compilaciones nocturnas con fecha 2019/07/28 o posterior](https://github.com/NightscoutFoundation/xDrip/releases).

* Desactive el receptor Dexcom original (si se utiliza).
* Pulse el icono xDrip+ en la gota de sangre de color rojo en la pantalla principal para habilitar el botón `Asistente de Origen`.
* Utilice el Botón Asistente de Origen que asegura la configuración predeterminada incluyendo OB1 & Modo Nativo 
   * Esto le guiará a través de la configuración inicial.
   * necesitará el número de serie del transmisor si es la primera vez que lo utiliza.

* Ponga el número de serie del nuevo transmisor (en el envase del transmisor o en la parte posterior del transmisor). Tenga cuidado de no confundir 0 (cero) y O (letra o mayúscula).
   
   ![xDrip+ Dexcom número de serie del Transmisor](../images/xDrip_Dexcom_TransmitterSN.png)

* Insertar nuevo sensor (sólo si se sustituye)

* Coloque el transmisor en el sensor
* No inicie un nuevo sensor antes de que se muestre la información siguiente en la página de estado clásica-> G5/G6 estado-> PhoneServiceState:
   
   * Transmisor con número de serie que empieza por 80 o 81: "Obtiene datos hh:mm" (por ejemplo, "Obtiene datos 19:04")
   * Transmisor con número de serie que empieza por 8G o 8H: "Got glucose hh:mm" (es decir, "Obtiene glucosa 19:04") o "No tengo ninguna hh:mm" (por ejemplo, "No tengo ninguna 19:04")
   
   ![xDrip PhoneServiceState](../images/xDrip_Dexcom_PhoneServiceState.png)

* Iniciar sensor (sólo si se reemplaza)
   
   -> Cerca de la parte inferior de la pantalla `Iniciando x, x horas faltantes` debe aparecer después de unos pocos minutos.

-> Si el número de serie de su transmisor no inicia con 8G o 8H y no hay una especificación de tiempo después de unos minutos para detener y reiniciar el sensor.

* Reiniciar el colector (estado del sistema - si no se reemplaza el sensor}
* No encienda el receptor original de Dexcom (si lo utiliza) de nuevo antes de xDrip+ muestre las primeras lecturas.
* Pulse el icono xDrip+ de goteo de sangre de color rojo en la pantalla principal para inhabilitar el `Botón Asistente de origen`.
   
   ![xDrip+ Dexcom Transmisor 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ Dexcom Transmisor 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ Dexcom Transmisor 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ Dexcom Transmisor 4](../images/xDrip_Dexcom_Transmitter04.png)

### Estado de la batería de Transmisor

* El estado de la batería se puede controlar en el estado del sistema (menú Hamburguesa en la parte superior izquierda de la pantalla de inicio)
* Deslizar la izquierda una vez para ver la segunda pantalla. ![xDrip+ First Transmisor 4](../images/xDrip_Dexcom_Battery.png)

* No se conocen los valores exactos cuando el transmisor "muere" debido a una batería vacía. La información siguiente se publicó en línea después de que el transmisor "murió":
   
   * Publicación 1: Día de transmisión: 151 / Voltaje A: 297 / Voltaje B: 260 / Resistencia: 2391
   * Publicación 2: Días de transmisión: 249 / Voltaje A: 275 (en tiempo de falla)

### Extender vida del transmisor

* Hasta ahora el tiempo de vida no se puede extender para los transmisores cuyo número de serie empieza por 8G o 8H.
* Para evitar las dificultades iniciando los sensores, se recomienda encarecidamente extender la vida del transmisor antes del día 100 de la primera utilización.
* La sesión en ejecución del sensor se detendrá al ampliar la vida del transmisor. Así que, extienda antes del cambio de sensor o tenga en cuenta que habrá una nueva fase de inicialización de 2 h.
* Cambie a la `modalidad de ingeniería`: 
   * pulsar sobre el carácter a la derecha de la pantalla de inicio de xDrip+ que representa una jeringa
   * luego toca el icono del micrófono en la esquina inferior derecha
   * En el recuadro de texto que abre escriba "enable engineering mode" 
   * pulse "Terminado"
   * Si el motor de Google Speak está habilitado, también puede hablar el comando de voz: "enable engineering mode". 
* Vaya a los valores de depuración G5 y compruebe `OB1 recopilador`.
* Utilice el mandato de voz: "hard reset transmitter"
* El comando de voz se ejecutará con la siguiente recepción de datos del transmisor
* Examine el estado del sistema (menú Hamburgesa-> estado del sistema) y consulte lo que sucede
* Si ve un mensaje "Phone Service State: Hard Reset habría fallado" en la segunda pantalla de estado del sistema, solo inicie el sensor y este mensaje debe desaparecer.
   
   ![xDrip+ El reseteo pudo haber fallado](../images/xDrip_HardResetMaybeFailed.png)

* Los días de Transmisor se establecerán en 0 después de la extensión y el inicio satisfactorios del sensor.

### Sustituir transmisor

Para los transmisores G6 fabricados después de otoño/finales de 2018 (es decir, con números de serie que empiezan por 80 u 81) por favor, asegúrate de utilizar la versión [maestra fechada 2019/05/18 ](https://jamorham.github.io/#xdrip-plus) o posterior.

Si el número de serie de su transmisor Dexcom G6 comienza con 8G u 8H utilizar una de las [últimas compilaciones nocturnas](https://github.com/NightscoutFoundation/xDrip/releases).

* Desactive el receptor Dexcom original (si se utiliza).
* Detener sensor (sólo si sustituye el sensor)
   
   Asegúrese de que realmente se ha detenido:
   
   En la segunda pantalla "Estado de G5/G6", mire a `Elementos de cola` aproximadamente en la mitad hacia abajo - Puede que diga algo como `(1) Detener sensor`
   
   Espere hasta que esto ocurra - normalmente en unos pocos minutos. El estado del sensor debe ser "Detenido" (consulte la captura de pantalla).
   
   -> Para quitar el transmisor sin detener el sensor ver este video <https://youtu.be/AAhBVsc6NZo>.
   
   ![xDrip+ Detener sensor Dexcom 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Detener sensor Dexcom 2](../images/xDrip_Dexcom_StopSensor2.png)

* Olvidar el dispositivo en estado del sistema de xDrip Y en la configuración BT del smartphone (¿Será mostrado como Dexcom?? mientras ?? son los dos últimos dígitos del número de serie del transmisor)
   
   ![xDrip+ Olvidar dispositivo](../images/xDrip_Dexcom_ForgetDevice.png)

* Retire el transmisor (y el sensor si reemplaza el sensor)

* Coloque el transmisor antiguo lejos para evitar la reconexión. Un microondas es un escudo de Faraday perfecto para esto, pero desenchufa el cable de alimentación para estar seguro al 100% de que nadie lo encienda.
* Pulse el icono xDrip+ en la gota de sangre de color rojo en la pantalla principal para habilitar el botón `Asistente de Origen`.
* Utilice el Botón Asistente de Origen que asegura la configuración predeterminada incluyendo OB1 & Modo Nativo 
   * Esto le guiará a través de la configuración inicial.
   * Necesitará el número de serie del transmisor si es la primera vez que lo utiliza.
* Introducir el número de serie del transmisor nuevo. Tenga cuidado de no confundir 0 (cero) y O (letra o mayúscula).
* Insertar nuevo sensor (sólo si se sustituye).
* Coloque el transmisor en el sensor - **No iniciar el sensor inmediatamente!**
* Nuevos "Transmisores Firefly" (número de serie que empiezan por 8G o 8H) sólo se pueden utilizar en la modalidad nativa.
* Las opciones siguientes no deben activarse para los nuevos "Transmisores Firefly" (número de serie que empiezan por 8G o 8H):
   
   * Reinicio preventivo (inhabilitar)
   * Reiniciar el sensor (deshabilitar!)
   * Volver a xDrip (deshabilitar!)
   
   ![Configuración de los transmisores Firefly](../images/xDrip_Dexcom_FireflySettings.png)

* Compruebe en la Página de Estado Clásica-> G5/G6 status-> PhoneServiceState si se muestra una de las siguientes informaciones:
   
   * Transmisor con número de serie que empieza por 80 o 81: "Obtiene datos hh:mm" (por ejemplo, "Obtiene datos 19:04")
   * Transmisor con número de serie que empieza por 8G o 8H: "Got glucose hh:mm" (es decir, "Obtiene glucosa 19:04") o "No tengo ninguna hh:mm" (por ejemplo, "No tengo ninguna 19:04")
   
   ![xDrip PhoneServiceState](../images/xDrip_Dexcom_PhoneServiceState.png)

* Espere 15 minutos ya que el transmisor debe comunicarse varias veces con xDrip antes de que se inicie el nuevo sensor. La batería de datos se muestra a continuación la información del Firmware.
   
   ![Datos de batería del transmisor firefly](../images/xDrip_Dexcom_FireflyBattery.png)

* ¡Inicie el sensor y NO PREDATE LA FECHA! Seleccione siempre "Sí, hoy"!

* Reiniciar el colector (estado del sistema - si no se reemplaza el sensor)
* No encienda el receptor original de Dexcom (si lo utiliza) de nuevo antes de xDrip+ muestre las primeras lecturas.
* Pulse el icono xDrip+ de goteo de sangre de color rojo en la pantalla principal para inhabilitar el `Botón Asistente de origen`.
   
   ![xDrip+ Dexcom Transmisor 1](../images/xDrip_Dexcom_Transmitter01.png)
   
   ![xDrip+ Dexcom Transmisor 2](../images/xDrip_Dexcom_Transmitter02.png)
   
   ![xDrip+ Dexcom Transmisor 3](../images/xDrip_Dexcom_Transmitter03.png)
   
   ![xDrip+ Dexcom Transmisor 4](../images/xDrip_Dexcom_Transmitter04.png)

### Nuevo Sensor

* Desactive el receptor Dexcom original (si se utiliza).
* Detener sensor si es necesario
   
   Asegúrese de que realmente se ha detenido:
   
   En la segunda pantalla "Estado de G5/G6", mire a `Elementos de cola` aproximadamente en la mitad hacia abajo - Puede que diga algo como `(1) Detener sensor`
   
   Espere hasta que esto ocurra - normalmente en unos pocos minutos.
   
   ![xDrip+ Detener sensor Dexcom 1](../images/xDrip_Dexcom_StopSensor.png)
   
   ![xDrip+ Detener sensor Dexcom 2](../images/xDrip_Dexcom_StopSensor2.png)

* Limpiar los contactos (lado trasero del transmisor) con alcohol y dejemos secar al aire.

* En caso de que utilice esta función, inhabilite `Reiniciar el sensor` y `Reinicios anticipados` (menú Hamburgesa-> Valores-> G5/G6 Depuración de valores). Si se pierda este paso y tiene estas funciones habilitadas, el nuevo sensor no se iniciará correctamente.
   
   ![xDrip+ Reinicio preventivo](../images/xDrip_Dexcom_Restart.png)

* Iniciar Sensor
   
   **Para los nuevos transmisores Firefly** (número de serie comenzando con 8G o 8H) **es obligatorio, para todos los demás transmisores se recomienda esperar aprox. 15 minutos entre parada y arranque el nuevo sensor (hasta `Estado de Sensor: Detenido` se muestra en la segunda pantalla de estado del sistema). NO PREDATE FECHAS!**

* Establecer tiempo insertado
   
   * Para utilizar el modo Nativo G6, debe esperar a que se inicie son 2 horas (por ejemplo, el tiempo de inserción es ahora).
   * Si utiliza el algoritmo xDrip+, puede establecer un tiempo anterior de más de 2 horas para evitar el inicio. Las lecturas pueden ser muy erráticas. Por lo tanto, esto no se recomienda.
* Introduzca el código del Sensor (en la lámina de papel de aluminio del sensor) 
   * Mantenga el código para futuras referencias (por ejemplo, un nuevo inicio después de que el transmisor haya tenido que eliminarse)
   * También se puede encontrar código en [xDrip+ logs ](../Configuration/xdrip#retrieve-sensor-code): pulse el menú de 3 puntos en la pantalla de inicio de xDrip+ y elija `Ver registros de sucesos`.
* No se necesita ninguna calibración si utiliza G6 en "modalidad nativa". xDrip+ mostrará las lecturas automáticamente después del inicio de 2 horas.
* No encienda el receptor original de Dexcom (si lo utiliza) de nuevo, antes de que xDrip+ muestre las primeras lecturas.
   
   ![xDrip+ Inicio Dexcom Sensor 1](../images/xDrip_Dexcom_SensorStart01.png)
   
   ![xDrip+ Inicio Dexcom Sensor 2](../images/xDrip_Dexcom_SensorStart02.png)

### Recuperar código de sensor

* En el maestro fechado 2019/05/18 y las últimas Versiones el código del sensor se muestra en el estado del sistema (la parte superior del menú de Hamburgesa que queda en la pantalla de inicio).
* Deslizar la izquierda una vez para ver la segunda pantalla.
   
   ![xDrip+ Recuperar código2 sensor Dexcom](../images/xDrip_Dexcom_SensorCode2.png)

* El código de sensor de Dexcom también se puede encontrar en los registros de xDrip+.

* Pulse el menú de 3 puntos (parte superior derecha en la pantalla de inicio)
* Seleccione `Ver registros de sucesos` y busque "código"
   
   ![xDrip+ Recuperar código sensor Dexcom](../images/xDrip_Dexcom_SensorCode.png)

## Solución de problemas de Dexcom G5/G6 y xDrip+

### Problema al conectar el transmisor

* El transmisor debe mostrarse en la configuración bluetooth de su smartphone.
* El transmisor se muestra como Dexcom?? mientras ?? representan los dos últimos dígitos del número de serie del transmisor (por ejemplo, DexcomHY).
* Abrir el estado del sistema en xDrip+ (menú hamburguesa en la parte superior izquierda de la pantalla de inicio).
* Compruebe si el transmisor se muestra en la primera página de estado ('página de estado clásico').
* Si no, elimine el dispositivo de la configuración bluetooth de su smartphone y reinicie el recolector.
* Espere unos 5 minutos. hasta que el transmisor Dexcom se vuelva a conectar automáticamente.

### Problema al iniciar un nuevo sensor

Por favor, tenga en cuenta que es posible que el siguiente método no funcione si el transmisor Dexcom G6 tiene el número de serie que empieza por 8G o 8H.

* El sensor nativo se marca como "FAILED: Sensor Failed Start"
* Detener Sensor
* Reinicia tu dispositivo
* Iniciar el sensor con el código 0000 (cuatro veces cero)
* Espere 15 minutos
* Detener Sensor
* Iniciar sensor con el código "real" (impreso en el protector adhesivo)

Consulte los registros de xDrip+ si xDrip+ inicia el conteo de "Duración: 1 minuto" (y siguiendo). Sólo en los registros de xdrip+ se puede detectar en una fase temprana si xdrip+ ha detenido un sensor. El estado más reciente no se muestra siempre correctamente en la parte inferior de la pantalla de inicio.

## xDrip+ & Freestyle Libre

### Libre configuración específica

* Abrir la Configuración Bluetooth -> Menú Hamburguesa (parte superior izquierda de la pantalla) -> Configuración -> desplácese hacia abajo -> Ajustes menos comunes -> Ajustes de Bluetooth
   
   ![xDrip+ Libre Configuración 1 de Bluetooth](../images/xDrip_Libre_BTSettings1.png)

* Habilite los siguientes parámetros
   
   * `Encender Bluetooth` 
   * `Usar escaneo`
   * `Siempre descubrir servicios`

* Todas las demás opciones deben ser desactivados
   
   ![xDrip+ Libre Configuración 2 de Bluetooth](../images/xDrip_Libre_BTSettings2.png)

### Conectar el transmisor de Libre & iniciar sensor

![xDrip+ iniciar transmisor Libre & Sensor 1](../images/xDrip_Libre_Transmitter01.png)

![xDrip+ iniciar transmisor Libre & Sensor 2](../images/xDrip_Libre_Transmitter02.png)

![xDrip+ iniciar transmisor Libre & Sensor 3](../images/xDrip_Libre_Transmitter03.png)