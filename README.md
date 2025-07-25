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
[acomprada en papelerías Folder](/images/cinta_doble_cara.png)

### Carcasa
- 4 tornillos M3x6
- 4 insertos metálicos [Length 4mm, M3 (OD 5mm)](https://es.aliexpress.com/item/1005004870993068.html?spm=a2g0o.order_list.order_list_main.17.506f194dqZ3Ccw&gatewayAdapt=glo2esp)

## Tiras led
Las tiras led compatibles con el firmware son: https://kno.wled.ge/basics/compatible-led-strips/
- La tira led que usamos en el taller es esta: [WS2813 DC5V, White PCB, 2m 60 IP65](https://es.aliexpress.com/item/1005004289391906.html?spm=a2g0o.order_list.order_list_main.10.5d6c194dSriMHZ&gatewayAdapt=glo2esp)
- Para la alimentación sirve cualquier cargador de móvil con carga rápida, IKEA tiene [estos](https://www.ikea.com/es/es/p/sjoss-cargador-usb-1-puerto-30-w-carga-rapida-50549412/) a muy buen precio
- [conectores hembra y macho JST SM de 4 pines](https://es.aliexpress.com/item/1005004615616698.html)


## Fabricación de stencil


## Flasheo y configuración de firmware WLED
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


## Autores
- [David Poza](http://github.com/davidpoza)
- [Jose David](http://github.com/jose8david)