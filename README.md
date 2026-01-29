# 🥇 S.I.G. Riego Pro: Planificador Hídrico Inteligente

Este repositorio contiene una herramienta avanzada de **ingeniería agronómica** diseñada para optimizar el uso del agua en cultivos leñosos. El sistema cruza datos climáticos históricos de **AEMET** con coeficientes de cultivo específicos para generar planes de riego precisos, incluso bajo restricciones de recursos hídricos.

## 🚀 Funcionalidades Clave

* **📍 Localización Geodésica**: Buscador de estaciones meteorológicas AEMET por coordenadas $XY$, calculando la distancia real en kilómetros mediante trigonometría esférica.
* **📊 Modelo Predictivo**: El sistema analiza los últimos 36 meses de datos históricos para generar un "Mes Tipo" de referencia basado en la media de Evapotranspiración (ETo) o Evaporación.
* **📅 Prorrateo Diario de Ciclo**: Permite definir fechas de inicio y fin de campaña exactas. La herramienta calcula el consumo proporcional según los días activos de cada mes (ajustando automáticamente meses de 28, 30 y 31 días).
* **🥇 Medalla de Oro Agronómica (Riego Deficitario)**: Lógica de prorrateo de dotación. Si el agua disponible es inferior a la demanda ideal, el sistema redistribuye los recursos de forma proporcional a la curva de necesidad del árbol, priorizando los momentos de máxima demanda.
* **🌳 Gestión de Dormancia**: Integración de una tabla maestra de $K_c$ para 25 tipos de frutales leñosos, aplicando consumo cero ($K_c=0$) en periodos de parada vegetativa (D).
* **🔍 Compatibilidad Multi-Variable**: Algoritmo de detección inteligente que procesa variables de AEMET como `eto_mes`, `evap_mes` o la evaporación directa `e`.



## 📐 Lógica Matemática

El sistema opera bajo las siguientes fórmulas de precisión:

1.  **Necesidad Ideal ($ET_c$):**
    $$ET_c (mm) = K_c(mes) \cdot \left( \frac{ETo_{mensual}}{días_{mes}} \cdot días_{activos} \right)$$

2.  **Conversión a Volumen:**
    $$V (m^3/ha) = ET_c (mm) \cdot 10$$

3.  **Prorrateo de Recursos (Riego Ajustado):**
    $$Riego_{mes} = \left( \frac{ETc_{mes}}{\sum ETc_{ciclo}} \right) \cdot Volumen_{Disponible}$$

## 🛠️ Stack Tecnológico

* **Frontend**: HTML5, CSS3 (Flexbox/Grid), JavaScript (ES6+).
* **Gráficos**: [Chart.js](https://www.chartjs.org/) para la visualización de balances.
* **Procesamiento de Datos**: [SheetJS (XLSX)](https://sheetjs.com/) para exportación de informes profesionales.
* **API**: Integración de datos desde AEMET OpenData.

---
*Desarrollado para la gestión eficiente del agua y la agricultura de precisión.*
