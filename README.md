# Sistema para Detección de EPP
**Integrantes:**
* Robles Garcia Juan Pablo (23310374)
* Medina Gonzalez Jose Ruben (23310341)

## Requisitos e Instalación
Para ejecutar y probar este proyecto, siga las siguientes instrucciones:

### 1. Ejecutar Google Colab
1. **Abrir Github:** Ingrese desde el enlace proporcionado en el repositorio al documento Jupyter Notebook (`.ipynb`). Esto lo redireccionará automáticamente a Google Colab, donde podrá visualizar el código fuente y el modelo entrenado YOLOv11.

2. **Tip:** Para maximizar la potencia del servidor y hacer que el entrenamiento del modelo sea mucho más rápido, se recomienda habilitar la aceleración por hardware. Vaya al menú superior: 
`Entorno de ejecución > Cambiar tipo de entorno de ejecución > GPU T4`

3. **Ejecutar el código** Ejecute todas las celdas de código de arriba hacia abajo para generar automáticamente los archivos de entrenamiento train, test y valid.

4. **Prueba de detección:** Podrá probar el funcionamiento del modelo ejecutando el siguiente comando:
   ```python
   res[6].show()

### 2. Detección Bonus
Si el usuario lo desea, en tiempo real se podrá visualizar el modelo YOLOv11 haciendo uso de la cámara integrada de su computadora, para ello descargue la carpeta con nombre: `Proyecto_Python_Vision_23310374_23310341`

Una vez descargada la carpeta, instale las librerias necesarias: `Ultralytics y Roboflow` dentro de Python ejecutando el siguiente comando:

pip install ultralytics roboflow opencv-python 

Para que el programa se pueda ejecutar en su totalidad, el programa abrirá una ventana emergente donde usted podrá visualizar en tiempo real cuando la cámara detecte si trae o no puesto el operador un chaleco de seguridad.

## Caso de Estudio
Se utilizo el modelo YOLOv11 de la familia YOLO para la deteccion de chalecos de seguridad (Equipo de Proteccion Personal) en entornos industriales de alto riesgo.
 
### 1. Objetivo
Automatizar el proceso de supervisión de los protocolos de seguridad con el fin de reducir el riesgo de accidentes laborales por descuido en el uso del EPP. 

### 2. Problemática
En zonas de alto riesgo industrial, sea maquinaria pesada, carga o construcción, el uso del chaleco de seguridad de alta visibilidad es obligatorio para evitar accidentes graves. La supervisión humana es propensa a cometer errores, por ende la falta de una alerta inmediata impide tomar medidas preventivas a tiempo.

### 3. Hardware Propuesto
Para llevar este modelo a la planta industrial, se requerirá de la siguiente infraestructura:
1. **Camaras de Seguridad:** De tipo IP estarán conectadas por cable Ethernet para garantizar transmisión de datos segura y eficiente. Deben tener resolución Full HD (1080p) y visión nocturna para operar en distintos turnos. Y, estarán instaladas en puntos estratégicos cubriendo los accesos a las zonas de alto riesgo.

2. **Servidor de Inferencia Local** Se contará con un servidor industrial equipado que cuente con un procesador especializado en IA (NVIDIA Jetson AGX Orin). Esto permitirá procesar los flujos de video localmente a alta velocidad sin la necesidad de depender de una conexión a internet externa.

3. **Infraestructura de Red** Un switch Gigabit PoE que interconectará las cámaras con el servidor de preferencia (Edge, Google, FireFox, etc.). El servidor contará con salida a la red local de la empresa para conectarse a un gateway de correo electrónico o a una app de mensajería para notificaciones móviles.

### 4. Flujo de Funcionamiento del Sistema
El comportamiento de este sistema autónomo sigue el siguiente ciclo lógico:

1. **Captura y Transmisión:** Las cámaras IP capturan de manera continua el entorno y transmiten el flujo de video en tiempo real mediante el protocolo hacia el servidor local.

2. **Conexión con YOLO:** El servidor procesa cada fotograma a través del `modelo YOLOv11` entrenado en este proyecto, el cual está capacitado para identificar y localizar de manera simultánea dos clases: `Vest y No-Vest`

3. **Lógica de Validación:** Un script en Python evalúa espacialmente las detecciones. Si el sistema detecta un cuadro delimitador de la clase No-Vest por un período continuo mayor a 5 segundos, el sistema activa el estado de "Infracción de Seguridad".

4. **Generación de Evidencia:** El software toma instantáneamente una captura de pantalla del fotograma exacto de la infracción, dibuja un recuadro alrededor del infractor con la etiqueta No-Vest junto con la fecha y hora exacta. 

5. **Envío de Alerta:** De forma asíncrona, el servidor invoca un servicio de mensajería o notificación utilizando la red interna o la app (Telegram, WhatsApp Business, etc.).

6. **Notificación al Supervisor:** El supervisor de seguridad recibe una captura de pantalla donde se visualiza claramente la falta del operario y mensaje con la siguiente estructura:

`¡ALERTA! Se ha detectado personal ingresando sin chaleco de seguridad a la zona`

7. **Medidas:** Al recibir la alerta visual y la ubicación en tiempo real, el supervisor puede intervenir inmediatamente para pedir la detención de las máquinas o del operario y así reducir el riesgo a accidentes.

## Evidencias
![img_uno](https://github.com/rubenmedinna/ProyectoPPE/blob/57f3af5c7d39fa83780970c019d66b8cd9728fa3/Proyecto%20Vision_Evidencias_23310341_23310374/Pruebas%20imagenes_23310341_23310374/Prueba10.png)

![img_dos](https://github.com/rubenmedinna/ProyectoPPE/blob/57f3af5c7d39fa83780970c019d66b8cd9728fa3/Proyecto%20Vision_Evidencias_23310341_23310374/Pruebas%20imagenes_23310341_23310374/Prueba12.png)

![img_tres](https://github.com/rubenmedinna/ProyectoPPE/blob/57f3af5c7d39fa83780970c019d66b8cd9728fa3/Proyecto%20Vision_Evidencias_23310341_23310374/Pruebas%20imagenes_23310341_23310374/Prueba8.png)