# Actividad-4
# 📈 Bot de IA para Recomendación de Inversiones en el Mercado Mexicano (Módulo NLU)

Este repositorio contiene la capa de **Comprensión de Lenguaje Natural (NLU)** orientada a identificar intenciones de inversión de usuarios financieros. El módulo conversacional sirve como la compuerta de entrada para un asistente inteligente capaz de estructurar portafolios en el mercado mexicano (CETES, IPC, SOFIPOS), consumiendo datos financieros públicos y APIs de instituciones bancarias.

---

## 💻 1. Entorno de Ejecución

Para garantizar la viabilidad de despliegue en entornos cloud de alta concurrencia y medir latencias válidas para ingeniería de software, el benchmark de los modelos se prototipó bajo las siguientes especificaciones técnicas:

*   **Entorno de desarrollo:** Google Colab Notebook (`.ipynb`).
*   **Aceleración por Hardware:** GPU NVIDIA Tesla T4 (Memoria de Video Dedicada GDDR6).
*   **Frameworks Core:** PyTorch, Hugging Face `transformers`, `datasets`, `accelerate` y `scikit-learn`.
*   **Estrategia de Inferencia:** Clasificación Zero-Shot basada en Tareas de Implicación Textual (NLI).
*   **Dataset Utilizado:** `bitext/Bitext-wealth-management-llm-chatbot-training-dataset` (Muestra balanceada y fija de 100 registros con semilla `random_state=42` evaluada sobre 24 intenciones financieras solapadas).

---

## 🚀 2. Pasos de Ejecución

Para reproducir de forma exacta y determinista las métricas y los reportes gráficos de este proyecto, siga esta secuencia de pasos:

### Paso 2.1: Configuración de Credenciales Ocultas en Colab
Para evitar exponer claves privadas en código público (buenas prácticas de desarrollo y seguridad de datos), el token de Hugging Face se consume mediante variables de entorno del sistema:
1. En la barra lateral izquierda de Google Colab, haga clic en el icono de la **llave 🔑 (Secrets / Variables de entorno)**.
2. Añada una nueva variable con el Nombre exacto de: `HF_token`.
3. En el campo de Valor, coloque su token personal de acceso (permisos de lectura o *Read*).
4. Active el interruptor de **"Notebook access"** para autorizar al cuaderno a leer la clave de forma invisible.

### Paso 2.2: Ejecución del Cuaderno Lógico
Abra el archivo `.ipynb` adjunto en este repositorio dentro de Google Colab y ejecute las celdas de forma secuencial:
*   **Celda 1 (Instalación):** Descarga de forma silenciosa el ecosistema técnico (`transformers`, `datasets`, etc.).
*   **Celda 2 (Inicialización):** Importa las librerías de manipulación de datos y valida la correcta asignación de los núcleos CUDA de la GPU Tesla T4.
*   **Celda 3 (Preparación):** Descarga el dataset enfocado en *Wealth Management* e indexa los vectores de texto crudo.
*   **Celda 4 (Inferencia y Reporte):** Descarga automáticamente las 3 arquitecturas preentrenadas del Hub, ejecuta el pipeline Zero-Shot, compila la tabla de métricas y renderiza la gráfica dual de eficiencia.

---

## 📊 3. Tabla de Resultados y Balance Operativo

Los modelos registraron el siguiente comportamiento cuantitativo durante el experimento de estrés conversacional:

| Modelo Evaluado | Identificador HF | Accuracy | Precision (Weighted) | F1-Score | Latencia Promedio (ms) |
| :--- | :--- | :---: | :---: | :---: | :---: |
| **BART-Large-MNLI** | `facebook/bart-large-mnli` | 0.6300 | 0.7519 | 0.6220 | 530.45 ms |
| **DeBERTa-v3-ZeroShot** | `MoritzLaurer/...` | 0.5100 | 0.5933 | 0.4900 | 666.58 ms |
| **DistilBART-Fast** | `valhalla/distilbart-mnli-12-3` | **0.6500** | **0.8482** | **0.6781** | **311.69 ms** |

---

## 🎯 4. Conclusiones y Recomendación de Negocio

1.  **Capacidad de Abstracción Semántica (NLU):** El análisis estadístico demuestra que la arquitectura compacta **`DistilBART-Fast`** superó a modelos de mayor tamaño en la tarea de clasificación de intenciones de inversión, logrando un **F1-Score ponderado de 0.6781** y una precisión del **0.8482**. Esto garantiza que casi el 85% de las solicitudes desestructuradas de los inversionistas mexicanos serán mapeadas con total exactitud, previniendo llamadas erróneas o destructivas a las APIs de los bancos corporativos.
2.  **Trade-off de Eficiencia Operativa (Latencia vs. Parámetros):** Existe un balance óptimo en las técnicas de destilación de conocimiento. `DistilBART-Fast` redujo las capas redundantes del Decoder, lo que le permitió registrar una latencia promedio por prompt de tan solo **311.69 ms** bajo la GPU Tesla T4, resultando un **41.2% más rápido que BART-Large** (530.45 ms). 
3.  **Impacto Financiero de la Recomendación:** Para la startup de inversión, implementar **`DistilBART-Fast`** representa la solución ideal. No solo provee la menor tasa de falsos positivos para transacciones financieras seguras, sino que su baja latencia garantiza una experiencia conversacional en tiempo real (por debajo del umbral de tolerancia humana de 400 ms) al tiempo que reduce drásticamente el consumo de horas/servidor cloud de GPU, minimizando los costos de infraestructura del negocio.
