![resultado final](/images/final_result.jpg)
Este proyecto nace de una práctica con Kicad en uno de los talleres de Makespace (slides de nuestro compañero Pablo Garrido [aquí](https://docs.google.com/presentation/d/1glYFRo9XCKRI-qDjp1DA8M3mJohLk-lrxx0JoBPsboM/edit?usp=drive_link)),
donde se diseñó el esquemático y el enrutado de la pcb para posterior fabricación de la misma en JLCPCB.

Continuando con el proceso lógico de aprendizaje, 
ahora este proyecto pretende servir como una primera aproximación en la práctica de soldadura SMD (componentes de montaje superficiales), 
así como fabricación de stencil usando una CNC (maquina de control numérico).

Junto al proyecto Kicad también se encuentran los stl de la carcasa para 

El repositorio con el proyecto Kicad: https://github.com/makespacemadrid/cheap-wled-controller718714


## BOM PCB
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

## BOM para Stencil
- [fresa 3.175mmx15Dx0.1, CN](https://www.aliexpress.com/item/4000966103866.html?spm=a2g0o.order_list.order_list_main.509.21ef194dDFnpwX)
- una lata de refresco


## Fabricación de stencil


## Flasheo y configuración de firmware WLED


## Software necesario
- [Kicad](https://www.kicad.org/): Diseño pcb y generación de gerbers.
- [Flatcam](http://flatcam.org/): **Solo windows (adjuntamos el gcode ya generado)** Creación de gcode a partir del gerber para la fabricación del stencil
- [gSender](https://sienci.com/gsender/?srsltid=AfmBOopYPgWM8177GG6Q0knLP97hrF1G2skJw3ewIg3omObme7XnkDx5): Comunicación con la CNC para enviar el gcode
- [OrcaSlicer](https://orca-slicer.com/): Cualquier slicer para impresora 3d para fabricar la carcasa.


## Autores
- [David Poza](http://github.com/davidpoza)
- [Jose David](http://github.com/jose8david)