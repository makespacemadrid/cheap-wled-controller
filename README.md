![resultado final](/images/final_result.jpg)
Este proyecto nace de una práctica con Kicad en uno de los talleres de Makespace (slides de nuestro compañero Pablo Garrido [aquí](https://docs.google.com/presentation/d/1glYFRo9XCKRI-qDjp1DA8M3mJohLk-lrxx0JoBPsboM/edit?usp=drive_link)),
donde se diseñó el esquemático y el enrutado de la pcb para posterior fabricación de la misma en JLCPCB.

Continuando con el proceso lógico de aprendizaje, 
ahora este proyecto pretende servir como una primera aproximación en la práctica de soldadura SMD (componentes de montaje superficiales), 
así como fabricación de stencil usando una CNC (maquina de control numérico).

Junto al proyecto Kicad también se encuentran los stl de la carcasa para imprimirla en 3d.

El repositorio con el proyecto Kicad: https://github.com/makespacemadrid/cheap-wled-controller718714

Esta pcb tiene la particularidad de usar para su alimentación un usb c con PD (Power delivery), lo que permite negociar diferentes votlajes y de este modo usar tiras led que trabajen a 5v, 9v, 12v, etc.

## BOM 
### PCB
- [CH224K USB PD Protocol Sink Chip IC 10Pcs/lot](https://www.aliexpress.com/item/1005005284290184.html?spm=a2g0o.order_list.order_list_main.5.21ef194dDFnpwX)
- [AMS1117 3.3](https://www.aliexpress.com/item/1005005350284100.html?spm=a2g0o.order_list.order_list_main.544.21ef194dDFnpwX)
- ESP32-S3-WROOM-1-N4R
- [TPS54202DDC](https://lcsc.com/product-detail/DC-DC-Converters_TI-TPS54202DDCR_C191884.html?s_z=n_C191884)
- [MX5014S](https://lcsc.com/product-detail/Gate-Drivers_Wuxi-Maxinmicro-MX5014S_C5359091.html?s_z=n_C5359091)
- [ESDA25W](https://lcsc.com/product-detail/ESD-and-Surge-Protection-TVS-ESD_TECH-PUBLIC-ESDA25W_C3021136.html?s_z=n_C3021136)
- [receptor IR](https://lcsc.com/product-detail/Infrared-Receivers_VISHAY_TSOP38238_TSOP38238_C141632.html)
- diodo led footprint 0805
- [conector usb C](https://lcsc.com/product-detail/USB-Connectors_Korean-Hroparts-Elec-TYPE-C-31-M-12_C165948.html?s_z=n_C165948)
- [pin-header](https://lcsc.com/product-detail/Pin-Headers_Megastar-ZX-PZ2-0-2-5PZZ_C7501288.html?s_z=n_C7501288)
- [mosfet canal N](https://lcsc.com/product-detail/MOSFETs_YANGJIE-YJG100N04A_C919580.html?s_z=n_C919580)

### Stencil
- [fresa 3.175mmx15Dx0.1, CN](https://www.aliexpress.com/item/4000966103866.html?spm=a2g0o.order_list.order_list_main.509.21ef194dDFnpwX)
- una lata de refresco
- cinta de carrocero
- cinta de doble cara sin espuma. La que usamos nosotros es esta, comprada en papelerías Folder:
[comprada en papelerías Folder](/images/cinta_doble_cara.png)

### Carcasa
- 4 tornillos M3x6
- 4 insertos metálicos [Length 4mm, M3 (OD 5mm)](https://es.aliexpress.com/item/1005004870993068.html?spm=a2g0o.order_list.order_list_main.17.506f194dqZ3Ccw&gatewayAdapt=glo2esp)

## Tiras led
Las tiras led compatibles con el firmware son: https://kno.wled.ge/basics/compatible-led-strips/
- La tira led que usamos en el taller es esta: [WS2813 DC5V, White PCB, 2m 60 IP65](https://es.aliexpress.com/item/1005004289391906.html?spm=a2g0o.order_list.order_list_main.10.5d6c194dSriMHZ&gatewayAdapt=glo2esp)
- Para la alimentación sirve cualquier cargador de móvil con carga rápida, IKEA tiene [estos](https://www.ikea.com/es/es/p/sjoss-cargador-usb-1-puerto-30-w-carga-rapida-50549412/) a muy buen precio
- [conectores hembra y macho JST SM de 4 pines](https://es.aliexpress.com/item/1005004615616698.html)


## Fabricación de stencil
Usaremos el software Flatcam, en el que cargamos la capa "paste top" del gerber que generamos en Kicad para enviar a fabricar la PCB.
Esta capa contiene la geometría de los pads de todos los componentes. 

El proceso lo vamos a llevar a cabo con una fresa de 30 grados y 0.1 de diámetro. Asumiendo que la lata de refresco tiene un grosor de 0.2mm.
Las capturas de los pasos a seguir son las siguientes:

![](/images/flatcam1.png)
![](/images/flatcam2.png)
![](/images/flatcam3.png)
![](/images/flatcam4.png)
![](/images/flatcam5.png)

El gcode generado finalmente lo hemos subido [aquí](/includes/paste_top.gcode).

## Flasheo y configuración de firmware WLED

### Flasheo

En nuestro caso estamos usando un esp32 s3 con 4MB, por lo que vamos a flashear desde la web: https://wled-install.github.io/

![alt text](/images/flashing.png)


### Configuración
En LED preferences:

La configuración de la tira:

![alt text](/images/led_config.png)

La configuración del mosfet para apagar la tira:

![alt text](/images/relay_config.png)

El botón en placa permite encender y apagar la tira manualmente:

![alt text](/images/button_config.png)

Para configurar el mando usaremos [este](/includes/18-key-ir.json) fichero json.

![alt text](/images/ir_config.png)

## Software necesario
- [Kicad](https://www.kicad.org/): Diseño pcb y generación de gerbers.
- [Flatcam](http://flatcam.org/): **Solo windows (adjuntamos el gcode ya generado)** Creación de gcode a partir del gerber para la fabricación del stencil
- [gSender](https://sienci.com/gsender/?srsltid=AfmBOopYPgWM8177GG6Q0knLP97hrF1G2skJw3ewIg3omObme7XnkDx5): Comunicación con la CNC para enviar el gcode
- [OrcaSlicer](https://orca-slicer.com/): Cualquier slicer para impresora 3d para fabricar la carcasa.

## Esquema de la placa

En este apartado se describen los componentes principales del circuito para gestionar la alimentación y regulación del voltaje de la tira LED.

---

### Información sobre el power delivery

📄 [UPD301A USB Power Delivery Operation](/datasheet/AN3265MicroChip.pdf)

📄 [A Primer on USB Type-C® and USB Power Delivery Applications and Requirements](/datasheet/PowerDeliveryTexas.pdf)

### 🔌 Conector USB-C

El conector USB-C que se utiliza en la placa tiene doce patillas con una separación muy pequeña entre cada una de ellas; además, en los dos extremos se encuentran los pines de alimentación (GND y VBUS), por lo que una mala soldadura podría generar un cortocircuito. 

![Connector](/images/footprint_USB.png)

> **Es importante que antes de conectar la placa se mida la resistencia entre los pines de alimentación para comprobar que no haya cortocircuito 🔥.**

---

### CH224K

El CH224K es el componente encargado de gestionar el protocolo *power delibery* (PD).

📄 [Descargar datasheet](https://github.com/makespacemadrid/cheap-wled-controller/blob/main/datasheet/ch224k.pdf)

- **Encapsulado:** ESSOP-10
- **Distribución de pines:**

  ![Pin](/images/ch224k_pin.png)



| Pin No.     | Pin name | Pin type          | Pin description                                                                 |
|-------------|----------|-------------------|----------------------------------------------------------------------------------|
| 0           | GND      | Power             | Ground. Heat dissipation EPAD.                                                  |
| 1           | VDD      | Power             | Operating power input. Requires external 1uF decoupling capacitor. Connected in series with a resistor to VBUS. |
| 4, 5        | DP, DM   | Input/Output      | USB data line                                                                   |
| 6, 7        | CC1, CC2 | Input/Output      | Type-C CC data line                                                             |
| 2, 3, 9     | CFG1, CFG2, CFG3 | Analog input     | Power configuration input                                                       |
| 8           | VBUS     | Analog input      | Voltage detection input. Connected in series with a resistor to external VBUS.  |
| 10          | PG       | Open-drain output | Indicates Power Good by default. Active low. Can be customized.                |


- **Configuración de voltaje de salida:**

  Los pines encargados de  configurar la salida del voltaje son el 2, el 3 y el 9. En este caso solo se utiliza el pin 9, por lo que en función de la resistencia que se conecte a este pin, el voltaje de salida variará entre 5 y 20 voltios.

  ![Schematic](/images/ch224k_david_schematic.png)

   >Por ejemplo, si se conecta una resistencia de 10 kΩ del pin 9 a tierra, el voltaje de salida (VBUS_CONN) será de 5 V.

  | Resistance on CFG to VDD | Request-voltage |
  |--------------------------|-----------------|
  | 10KΩ                     | 5V              |
  | 20KΩ                     | 9V              |
  | 47KΩ                     | 12V             |
  | 100KΩ                    | 15V             |
  | 200KΩ                    | 20V             |


---
### TPS54202

El voltaje que sale del CH224K entra en el *buck converter* TPS54202, que será el encargado de generar los 5 voltios estables del circuito.

📄 [Descargar datasheet](/datasheet/tps54202.pdf)

- **Encapsulado:** SOT-23
  
- **Distribución de pines:**

  ![Distribución de pines TPS54202](/images/tps54202_pin.png)

- **Configuración del circuito:**
  
  En el esquema del circuito se puede observar la configuración del componente, compuesta por resistencias, condensadores y la bobina L2, que mediante su carga (en forma de campo magnético) y descarga genera la corriente necesaria para alimentar los condensadores, que estabilizarán los 5 voltios de salida (+5V).

  ![Schematic](/images/tps54202ddc.png)

---
### AMS1117 3-3V

Una vez que se ha generado el voltaje +5V, el regulador de voltaje lineal (LDO) AMS1117 comienza a trabajar para entregar los 3,3V. Hay que tener en cuenta que la corriente máxima que puede entregar este regulador es de 1A. 

📄 [Descargar datasheet](/datasheet/ams1117.pdf)

- **Distribución de pines:**

  ![Distribución de pines AMS1117](/images/ams1117_pin.png)

  > PIN 1: GND
  >
  > PIN 2: VOUT
  >
  > PIN 3: VDD

- **Configuración del circuito:**
  
  ![Schematic](/images/AMS1117.png)

---
### ESP32-S3-WROOM-1-N4R2

📄 [Descargar datasheet](/datasheet/esp32-s3.pdf)

- **Distribución de pines:**

  ![Distribución de pines ESP32-S3-WROOM-1-N4R2](/images/esp32_pin.png)

- **Configuración del circuito:**
  
  ![Schematic](/images/esp32_schematic.png)

---
### MX5014S

 La tira LED se alimenta a través del voltaje que se genera en el MOSFET Q3, que está controlado por el MX5014S, y que a su vez responde del IO47 del ESP32.

📄 [Descargar datasheet](/datasheet/mx5014s.pdf)

- **Distribución de pines:**
  
  ![Distribución de los pines](/images/mx5014s_pin.png)

- **Configuración del circuito:**
  
  ![Schematic](/images/mx5014s_schematic.png)

## Líneas de voltaje principales

|Línea|Voltaje|Componente|
|-----|-------|----------|
|V_LED_|5-20V|CH224K|
|+5V|5V|TPS54202|
|+3.3V|3.3V|AMS1117|
|LED_1_VCC|5-20V|Q3

---
## Stencil con los valores de los componentes

![Stencil](/images/stencil_components_values.png)

![Stencil](/images/stencil_components_values_color.png)
---
## Autores
- [David Poza](http://github.com/davidpoza)
- [Jose David](http://github.com/jose8david)
