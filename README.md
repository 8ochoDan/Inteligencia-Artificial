#INTELIGENCIA ARTIFICIAL
-------7. Tilines - PROYECTO: SISTEMA DE RECONOCIMIENTO DE OBJETOS CON APRENDIZAJE INCREMENTAL APLICADO  A ROVER DE CONDUCCIÓN AUTÓNOMA BÁSICA----------
Integrante 1 - Ana Laura Santiago Morales - Ani
Responsabilidades dentro del equipo: Por discutir.
Herramientas, lenguajes de programación, módulos de los que se hará cargo: Por discutir.

Integrante 2 - Daniel Alfredo Ochoa González - ocho
Responsabilidades dentro del equipo: Por discutir.
Herramientas, lenguajes de programación, módulos de los que se hará cargo: Por discutir.

Integrante 3 - Jesus Salvador Juárez Cruz - Chuy
Responsabilidades dentro del equipo: Por discutir.
Herramientas, lenguajes de programación, módulos de los que se hará cargo: Por discutir.

Integrante 4 - Monserrat Martínez López - mon
Responsabilidades dentro del equipo: Por discutir.
Herramientas, lenguajes de programación, módulos de los que se hará cargo: Por discutir.

1.- Propuesta general: Nuestro proyecto resuelve el problema de dotar de percepción visual inteligente y personalizable a un robot rover de bajo costo, permitiéndole reconocer objetos específicos del entorno donde se desenvuelve sin necesidad de reentrenar modelos desde cero ni depender de hardware caro. El problema real es que los robots educativos actuales no pueden adaptarse rápidamente a nuevos objetos (señales, obstáculos, personas) sin un proceso de reentrenamiento complejo y costoso.

usuario final: Nosotros mismos. El sistema será implementado directamente en un rover físico construido por algunos integrantes del equipo. No buscamos un usuario externo en esta etapa, sino validar el sistema en un robot propio como prueba de concepto funcional.

Proyectos parecidos:Existen proyectos como DonkeyCar, JetBot (NVIDIA) y OpenCV AI Kit. Sin embargo, estos proyectos asumen que el usuario tiene conocimientos avanzados de ML o hardware específico. Nuestro diferencial es que integramos una API de reconocimiento con capacidad de aprendizaje incremental en un rover económico, algo que no existe orientado a estudiantes de nuestra ciudad ni con la facilidad de uso que proponemos.

2.- Arquitectura y herramientas
Tipos de IA a usar:Usaremos principalmente visión por computadora mediante modelos de detección de objetos (YOLO). No usaremos LLMs ni IA generativa en el núcleo del sistema. Opcionalmente, podríamos integrar NLP para etiquetado por voz en el futuro.

API en linea o modelo local: Usaremos un modelo local open source (YOLO) ejecutándose en un servidor propio o en una laptop del equipo. La razón es que necesitamos control total sobre el fine-tuning y no queremos depender de costos de API ni de conexión a internet en el robot. El ESP32-S3-CAM del rover se comunicará con este servidor vía WiFi para enviar imágenes y recibir detecciones.

Back, Front y Base:
 	Backend: FastAPI (Python) — integración nativa con PyTorch y Ultralytics YOLO.
 	Frontend: React + Next.js — para la interfaz web de etiquetado y monitoreo.
 	Base de datos: PostgreSQL + MinIO — PostgreSQL para metadatos relacionales, MinIO para almacenar imágenes.
Elegimos estas tecnologías por su madurez, documentación abundante y compatibilidad con el ecosistema de IA.

Parte riesgosa técnicamente: La parte más riesgosa es lograr que el rover ejecute inferencia en tiempo real sin latencia excesiva. El ESP32-S3-CAM envía imágenes por WiFi al servidor, y la respuesta debe llegar en milisegundos para que el robot reaccione a tiempo. Si el WiFi falla o la latencia es alta, el robot podría no reaccionar bien. También es riesgoso mantener la precisión del modelo tras el fine-tuning incremental.

Probar funcionalidad: Probaremos en tres niveles: unitario (pruebas automatizadas de la API), funcional (con imágenes pregrabadas para validar detecciones) y real (el rover físico navegando en un circuito con obstáculos y señales reales). Mediremos la tasa de detección correcta y el tiempo de respuesta del sistema completo en condiciones reales

3.- Alcance y entregables 
Version minima viable (MVP): El MVP consiste en un rover funcional que se mueve de forma autónoma, enviando imágenes desde su cámara al servidor, recibiendo detecciones de objetos (al menos 2-3 clases: por ejemplo, "persona", "obstáculo" y "señal de alto"), y ejecutando maniobras básicas: detenerse ante un obstáculo y girar cuando detecta un objeto a un lado. No incluye aprendizaje incremental en esta fase.
 Entregables al final:
 	Código fuente del backend (API + scripts de entrenamiento) en GitHub.
 	Código del firmware del ESP32-S3-CAM.
 	Documentación técnica (README + TRS).
 	Video demostrativo del rover navegando de forma autónoma.
 	Presentación con arquitectura y resultados
 	El rover detecta correctamente al menos el 65% de los objetos en un circuito de prueba controlado.
 	El tiempo de respuesta (captura → detección → comando a motores) es menor a 8 segundos.
 	La API responde correctamente en el 80% de las solicitudes durante las pruebas

Entregables opcionales (si sobra tiempo)
 	Aprendizaje incremental funcional: poder añadir nuevas clases desde el cliente web y reentrenar el modelo.
 	Cliente móvil (React Native) para monitorear el rover en tiempo real.
 	Panel de visualización con las detecciones superpuestas en video.
 	Integración de sensor ultrasónico para refuerzo de seguridad a corta distancia.
 	Exportación de datasets para que otros equipos reutilicen los datos etiquetados.
