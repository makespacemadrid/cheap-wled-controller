# Esquema de la placa

En este apartado se describen los componentes principales del circuito para gestionar la alimentación y regulación del voltaje de la tira LED.

---

## 🔌 Conector USB-C

El conector USB-C que se utiliza en la placa tiene doce patillas con una separación muy pequeña entre cada una de ellas, además en los dos extremos se encuentran los pines de alimentación (GND y VBUS), por lo que una mala soldadura podría generar un cortocircuito. 

![Connector](/images/footprint_USB.png)

> **Es importante que antes de conectar la placa se mida la resistencia entre los pines de alimentación para comprobar que no haya cortocircuito 🔥.**

---

## CH224K

El CH224K es el componente encargado de gestionar el protocolo power delibery (PD).

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
## TPS54202

El voltaje que sale del CH224K entra en el buck converter TPS54202, que será el encargado de generar los 5 voltios estables del circuito.

📄 [Descargar datasheet](/datasheet/tps54202.pdf)

- **Encapsulado:** SOT-23
  
- **Distribución de pines:**

  ![Distribución de pines TPS54202](/images/tps54202_pin.png)

- **Configuración del circuito:**
  
  En el esquema del circuito se puede observar la configuración del componente, compuesta por resistencias, condensadores y la bobina L2, que mediante su carga (en forma de campo magnético) y descarga genera la corriente necesaria para alimentar a los condensadores, quienes estabilizarán los 5 voltios de salida (+5V)

  ![Schematic](/images/tps54202ddc.png)

---
## AMS1117 3-3V

Una vez que se ha generado el voltaje +5V, el regulador de voltaje lineal (LDO) AMS1117 comienza a trabajar para entregar los 3,3V. Hay que tener en cuenta que, la corriente máxima que puede entregar este regulador es de 1A. 

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
## ESP32-S3-WROOM-1-N4R2

📄 [Descargar datasheet](/datasheet/esp32-s3.pdf)

- **Distribución de pines:**

  ![Distribución de pines ESP32-S3-WROOM-1-N4R2](/images/esp32_pin.png)

- **Configuración del circuito:**
  
  ![Schematic](/images/esp32_schematic.png)


---
## MX5014S

 La tira LED se alimenta a través del voltaje que se genera en el mosfet Q3, que está controlado por el MX5014S, quien a su vez responde del IO47 del ESP32.

📄 [Descargar datasheet](/datasheet/mx5014s.pdf)

- **Distribución de pines:**
  
  ![Distribución de los pines](/images/mx5014s_pin.png)

- **Configuración del circuito:**
  
  ![Schematic](/images/mx5014s_schematic.png)

# Líneas de voltaje principales

|Línea|Voltaje|Componente|
|-----|-------|----------|
|V_LED_|5-20V|CH224K|
|+5V|5V|TPS54202|
|+3.3V|3.3V|AMS1117|
|LED_1_VCC|5-20V|Q3