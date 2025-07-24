### Esquema de la placa

En esta sección se describen los componentes principales que integran la placa. 

#### CH224K

El componente encargado del power delibery (PD) es el CH224K.

El datasheet del componente lo podéis encontrar aquí [Datasheet](https://github.com/makespacemadrid/cheap-wled-controller/blob/main/datasheet/ch224k.pdf)

El encapsulado del componente es el **ESSOP-10** y la distribución de pines es la siguiente

![Pin](/images/ch224k_pin.png)

Las funciones de cada uno de los pines son las siguientes

![Pin description](/images/ch224k_pin_description.png)

Los pines encargados de  configurar la salida del voltaje son el 2, el 3 y el 9. En este caso solo se utiliza el pin 9 para este fin.

![Schematic](/images/ch224k_david_schematic.png)

En función de la resistencia que se conecte al pin 9, el voltaje de salida variará.

![Resistor](/images/ch224k_config_resistances.png)

#### 