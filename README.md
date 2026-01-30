# 💧 S.I.G. Riego Pro (Sistema Integral de Gestión de Riego)

**Versión 1.0 (Estable)**

Una herramienta web avanzada de ingeniería agronómica diseñada para el cálculo, planificación y gestión eficiente de recursos hídricos en agricultura. Transforma datos climáticos históricos en planes de riego operativos, aplicando normativas internacionales (USDA, FAO) y lógica de balance hídrico neto.

---

## 🚀 Funcionalidades Clave

### 📍 1. Geolocalización y Climatología
* **Búsqueda Geoespacial:** Algoritmo que identifica automáticamente la estación meteorológica (AEMET) más cercana a las coordenadas exactas de la parcela.
* **Base Cartográfica y Geodesia:** El sistema opera bajo el estándar **EPSG:4258** (ETRS89 en coordenadas geográficas Latitud/Longitud), garantizando plena compatibilidad con la cartografía oficial española y europea.
* **Cálculo de Proximidad:** Se implementa una **Aproximación Euclidiana** sobre el plano ($d = \sqrt{\Delta lat^2 + \Delta lon^2} \times 111$) utilizando el factor de conversión estándar de 111 km/grado. Esta aproximación optimiza el rendimiento computacional en el cliente, ofreciendo una precisión submétrica en distancias locales frente a fórmulas geodésicas complejas.
* **Procesamiento de Datos:** Ingesta de archivos JSON (formato AEMET OpenData) para el análisis de series climáticas históricas.

### 🔮 2. Modelo Climático Predictivo (Patrón de Referencia)
Dado que la gestión agronómica requiere anticiparse a las necesidades de la campaña, el sistema implementa un motor de proyección basado en estadística climática reciente:
* **Generación del "Año Tipo":** El software no utiliza un único año (que podría ser atípico), sino que procesa los datos del archivo JSON para extraer la **media aritmética mensual** de los últimos 3 años disponibles.
* **Fiabilidad del Balance:** Al promediar un trienio, se establece un patrón de referencia robusto para la **ET<sub>0</sub>** y la **Precipitación**. Esto permite que, aunque el ciclo de cultivo se configure para fechas futuras, el balance hídrico se sustente sobre una base científica que suaviza anomalías térmicas o pluviométricas puntuales.
* **Estacionalidad:** El modelo respeta la estacionalidad climática local de la estación de AEMET seleccionada, asegurando que la curva de demanda hídrica sea coherente con el entorno real de la finca.

### 🥇 3. Balance Hídrico Mensual (Agronómico)
El núcleo del sistema se basa en la metodología del **Riego Neto**:
* **Cálculo de ET<sub>c</sub>:** Determinación de la Evapotranspiración del cultivo mediante la interacción de la ET<sub>o</sub> climática y Coeficientes de Cultivo (**K<sub>c</sub>**) dinámicos.
* **Precipitación Efectiva (P<sub>e</sub>):** Implementación del **Método USDA (SCS)** modificado para cuantificar la lluvia útil almacenada en la zona radicular:
    * *Si P < 70 mm:* **P<sub>e</sub> = 0.6 · P - 10**
    * *Si P > 70 mm:* **P<sub>e</sub> = 0.8 · P - 24**
* **Necesidad Hídrica Neta (NH<sub>n</sub>):** Cálculo preciso del déficit real del cultivo resultante del balance hídrico (**ET<sub>c</sub> - P<sub>e</sub>**).
* **Gestión de Recursos:** Algoritmo de reparto proporcional basado en una **Estrategia de Riego Deficitario Controlado**; este sistema ajusta automáticamente la dotación final cuando el volumen disponible es inferior a la demanda **NH<sub>n</sub>** ideal, optimizando la productividad por m³.
### 📅 4. Planificación Operativa Semanal
* **Flujo Continuo:** Conversión de la planificación mensual a semanas naturales del año (ISO 8601).
* **Distribución Diaria:** Lógica de interpolación diaria que evita los "escalones" o cortes artificiales entre meses, generando una curva de riego suave, continua y agronómicamente viable.

### 📊 5. Visualización y Reporting
* **Dashboard Interactivo:** Gráficos profesionales (Chart.js) con diseño optimizado:
    * **Azul Cielo (`#38bdf8`):** Precipitación Efectiva (P<sub>e</sub>).
    * **Azul Real (`#2563eb`):** Necesidad Neta (NH<sub>n</sub>).
    * **Oro/Ámbar (`#d97706`):** Riego Asignado (Recurso Humano).
* **Exportación de Datos:** Generación automática de informes en Excel (`.xlsx`) con tablas detalladas para el cuaderno de campo.

---

## 📐 Lógica Matemática del Balance

1.  **Demanda del Cultivo (ET<sub>c</sub>):**
    $$ET_c = ET_0 \times K_c$$
2.  **Necesidad Hídrica Neta (NH<sub>n</sub>):**
    $$NH_n = Max(0, ET_c - P_e)$$
3.  **Factor de Déficit (K<sub>s</sub>):**
    $$K_s = \frac{Volumen\ Disponible}{\sum NH_n}$$
4.  **Riego Final Asignado:**
    $$Riego = NH_n \times K_s$$

---

## 🛠️ Tecnologías y Diseño

* **Frontend:** HTML5, CSS3, Vanilla JavaScript (ES6+).
* **Motor Gráfico:** Chart.js + Plugin DataLabels (Estilo personalizado con tooltips modernos).
* **Motor de Datos:** SheetJS (XLSX) para la generación de hojas de cálculo.
* **UI/UX:** Diseño "Clean Card" inspirado en interfaces modernas, con una paleta de colores semántica que diferencia claramente los aportes hídricos naturales de los artificiales.

---

> **Nota:** Este proyecto ha sido desarrollado siguiendo estrictos criterios agronómicos para ofrecer una herramienta de precisión a técnicos y gestores de fincas.
> 
> **Estado del Proyecto:** ✅ Versión Estable 1.0
