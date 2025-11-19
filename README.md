# GestureGuide - Traductor de Lenguaje de Señas

## Descripción del Proyecto

ConnectSigns es una aplicación de inteligencia artificial que traduce lenguaje de señas a texto en tiempo real. Este sistema utiliza tecnologías avanzadas de visión por computadora y aprendizaje profundo para detectar y reconocer gestos del lenguaje de señas, facilitando la comunicación entre personas con discapacidad auditiva y el resto de la comunidad.

El proyecto combina MediaPipe para la detección de poses y movimientos de manos, TensorFlow/Keras para el procesamiento de machine learning, y Flask para el desarrollo de la aplicación web, creando una solución integral y accesible.

## Características Principales

- **Traducción en tiempo real**: Convierte gestos del lenguaje de señas a texto instantáneamente
- **Interfaz web intuitiva**: Aplicación desarrollada con Flask y Bootstrap para facilidad de uso
- **Detección avanzada de gestos**: Utiliza MediaPipe para extraer puntos clave de poses y manos
- **Síntesis de voz**: Convierte el texto traducido a audio usando Google Text-to-Speech
- **Compatibilidad multiplataforma**: Funciona en cualquier navegador web con soporte para cámara
- **Procesamiento de video**: Capacidad de procesar tanto video en tiempo real como archivos de video

## Arquitectura del Sistema

### Componentes Principales

```
SignLanguageTranslator/
├── app.py                 # Aplicación principal Flask
├── funtions.py           # Funciones auxiliares de procesamiento
├── metrics.py            # Extracción de métricas de gestos
├── models/               # Modelos de machine learning
│   └── modelfinal1.keras
├── templates/            # Plantillas HTML
│   ├── index.html
│   ├── service-details.html
│   ├── starter-page.html
│   └── tutorial-page.html
├── static/               # Recursos estáticos
│   ├── assets/
│   │   ├── css/
│   │   ├── js/
│   │   └── img/
│   └── vendor/           # Librerías frontend
└── requeriments.txt      # Dependencias del proyecto
```

### Flujo de Procesamiento

1. **Captura de Video**: La aplicación accede a la cámara web del usuario o procesa videos subidos
2. **Detección de Keypoints**: MediaPipe extrae puntos clave de pose corporal y manos
3. **Secuenciado**: Se analizan secuencias de 15 frames para capturar gestos completos
4. **Predicción**: Un modelo LSTM procesa las secuencias y predice la palabra/frase correspondiente
5. **Salida Multimodal**: El resultado se muestra como texto y se reproduce como audio

## Tecnologías Utilizadas

### Backend

- **Flask**: Framework web principal
- **Flask-CORS**: Manejo de Cross-Origin Resource Sharing
- **TensorFlow/Keras**: Framework de machine learning
- **OpenCV**: Procesamiento de imágenes y video
- **MediaPipe**: Detección de poses y gestos corporales
- **NumPy**: Computación numérica y manejo de arrays

### Frontend

- **HTML5/CSS3**: Estructura y estilos
- **JavaScript**: Interactividad del lado cliente
- **Bootstrap**: Framework CSS para diseño responsivo
- **Vendor Libraries**: AOS, GLightbox, Swiper, etc.

### Servicios Adicionales

- **Google Text-to-Speech (gTTS)**: Síntesis de voz
- **Pygame**: Reproducción de audio
- **Werkzeug**: Utilidades web adicionales

## Requisitos del Sistema

### Requisitos de Software

- **Python**: 3.11 o superior
- **Sistema Operativo**: Windows, macOS, o Linux
- **Navegador Web**: Chrome, Firefox, Safari, Edge (con soporte para WebRTC)
- **Cámara Web**: Para funcionalidad en tiempo real

### Requisitos de Hardware

- **RAM**: Mínimo 4GB, recomendado 8GB
- **Procesador**: CPU de doble núcleo o superior
- **Espacio en Disco**: 2GB libres para dependencias
- **Cámara**: Cámara web integrada o USB con resolución mínima 640x480

## Instalación y Configuración

### 1. Clonar el Repositorio

```bash
git clone https://github.com/YoelMantari/SignLanguageTranslattor.git
cd SignLanguageTranslattor
```

### 2. Crear Entorno Virtual

Es altamente recomendado usar un entorno virtual para evitar conflictos de dependencias:

```bash
py -3.11 -m venv .venv
```

### 3. Activar el Entorno Virtual

**En Windows:**

```bash
.venv\Scripts\activate
```

**En macOS/Linux:**

```bash
source .venv/bin/activate
```

### 4. Instalar Dependencias

```bash
pip install -r requeriments.txt
```

**Nota**: La instalación puede tomar varios minutos debido al tamaño de las librerías de machine learning.

### 5. Verificar la Instalación

Puedes verificar que las dependencias principales estén instaladas correctamente:

```bash
python -c "import tensorflow, cv2, mediapipe; print('Instalación exitosa')"
```

### 6. Ejecutar la Aplicación

```bash
python app.py
```

La aplicación estará disponible en: `http://127.0.0.1:5000`

## Uso de la Aplicación

### Interfaz Web

1. **Página Principal**: Navegue a `http://127.0.0.1:5000` en su navegador
2. **Permitir Acceso**: Autorice el acceso a la cámara web cuando se solicite
3. **Detección en Tiempo Real**: Coloque sus manos frente a la cámara
4. **Visualización**: Los gestos detectados aparecerán como texto en pantalla
5. **Audio**: El texto será convertido automáticamente a voz

### API Endpoints

La aplicación también proporciona una API REST:

- `POST /predict`: Procesa un archivo de video y retorna la predicción
- `GET /`: Página principal
- `GET /tutorial-page`: Página de tutorial
- `GET /service-details`: Detalles del servicio

### Procesamiento de Video

Para procesar archivos de video, puede usar el endpoint `/predict`:

```bash
curl -X POST -F "video=@mi_video.mp4" http://127.0.0.1:5000/predict
```

## Configuración Avanzada

### Parámetros del Modelo

El sistema utiliza los siguientes parámetros configurables en `app.py`:

- `MAX_LENGTH_FRAMES = 15`: Máximo número de frames por secuencia
- `MIN_LENGTH_FRAMES = 5`: Mínimo número de frames requeridos
- `LENGTH_KEYPOINTS = 258`: Número de puntos clave extraídos por frame

### Umbral de Confianza

El modelo utiliza un umbral de confianza de 0.7 por defecto. Puede ajustarse en la función `evaluate_model()`.

## Solución de Problemas

### Problemas Comunes

**Error de cámara no detectada:**

- Verifique que la cámara esté conectada y funcionando
- Cierre otras aplicaciones que puedan estar usando la cámara
- Verifique los permisos del navegador para acceder a la cámara

**Error de importación de TensorFlow:**

- Asegúrese de estar usando Python 3.11
- Verifique que el entorno virtual esté activado
- Reinstale TensorFlow: `pip uninstall tensorflow && pip install tensorflow==2.16.2`

**Rendimiento lento:**

- Cierre aplicaciones innecesarias
- Verifique que su sistema cumpla con los requisitos mínimos
- Considere usar una GPU compatible con TensorFlow

### Logs y Debugging

Para habilitar logs detallados, ejecute la aplicación con:

```bash
python app.py --debug
```

## Contribución al Proyecto

### Configuración para Desarrollo

1. Fork el repositorio
2. Cree una rama para su feature: `git checkout -b feature/nueva-funcionalidad`
3. Realice sus cambios y pruebas
4. Commit sus cambios: `git commit -m 'Agregar nueva funcionalidad'`
5. Push a la rama: `git push origin feature/nueva-funcionalidad`
6. Abra un Pull Request

### Estándares de Código

- Siga las convenciones PEP 8 para Python
- Agregue comentarios descriptivos para funciones complejas
- Incluya pruebas para nuevas funcionalidades
- Actualice la documentación según sea necesario

## Créditos y Licencia

### Desarrolladores

Este proyecto fue desarrollado por estudiantes de la Universidad Nacional de Ingeniería como parte del curso de Interacción Humano-Computadora:

- Yoel Mantari
- Mitchel Soto
- Ivan Urbano

### Licencia

Este proyecto está licenciado bajo la Licencia MIT. Consulte el archivo [LICENSE](LICENSE) para más detalles.

### Agradecimientos

- MediaPipe by Google para las herramientas de detección de poses
- TensorFlow/Keras para el framework de machine learning
- Bootstrap team para el framework CSS
- Comunidad de código abierto por las librerías utilizadas

## Versión

**Versión actual**: 1.0.0  
**Última actualización**: Noviembre 2025
