### Esquema de la placa

En esta sección se describen los componentes principales del circuito. 

#### Conector USB-C

El conector USB-C que se utiliza en la placa tiene doce patillas con una separación muy pequeña entre cada una de ellas, además en los dos extremos se encuentran los pines de alimentación (GND y VBUS), por lo que una mala soldadura podría generar un cortocircuito. 

![Connector](/images/footprint_USB.png)

Es importante que antes de conectar la placa se mida la resistencia entre los pines de alimentación para asegurar que no haya cortocircuito.

#### CH224K

El componente encargado del power delibery (PD) es el CH224K.

El datasheet del componente se puede descargar aquí [Datasheet](https://github.com/makespacemadrid/cheap-wled-controller/blob/main/datasheet/ch224k.pdf)

El encapsulado del componente es el **ESSOP-10** y la distribución de sus pines es la siguiente:

![Pin](/images/ch224k_pin.png)

Las funciones de cada uno de los pines se detallan a continuación:

![Pin description](/images/ch224k_pin_description.png)

Los pines encargados de  configurar la salida del voltaje son el 2, el 3 y el 9. En este caso solo se utiliza el pin 9 para este fin.

![Schematic](/images/ch224k_david_schematic.png)

En función de la resistencia que se conecte al pin 9, el voltaje de salida variará. Por ejemplo, si se conecta una resistencia de 10 kΩ del pin 9 a tierra, el voltaje de salida (VBUS_CONN) será de 5 V.

![Resistor](/images/ch224k_config_resistances.png)

#### TPS54202

El voltaje que sale del CH224K entra en el buck converter TPS54202, con un rango de voltaje de entrada entre los 4,5 V a los 28 V, y cuyo datasheet se puede descargar aqui [Datasheet](/datasheet/tps54202.pdf)

El encapsulado del componente es el **TPS54202** y la distribución de sus pines es la siguiente:

![Pin](/images/tps54202_pin.png)

En el esquema del circuito se puede observar la configuración del componente:

![Schematic](/images/tps54202ddc.png)

