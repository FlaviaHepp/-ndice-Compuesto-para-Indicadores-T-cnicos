# 📈 Índice Compuesto para Indicadores Técnicos

## 📌Descripción del Proyecto

Este proyecto implementa un índice compuesto optimizado sobre la tabla indicadores_tecnicos, diseñado para acelerar consultas analíticas basadas en series temporales por activo financiero.

El índice está orientado a workloads típicos de análisis cuantitativo, donde se consultan indicadores técnicos (RSI, SMA, kurtosis, skewness, etc.) por ticker y en orden cronológico, priorizando los datos más recientes.

## 📍Objetivo

Mejorar significativamente el rendimiento de consultas que:
- Filtran por ticker_id
- Ordenan por fecha (especialmente fechas recientes)
- Utilizan funciones de ventana (LAG, LEAD, AVG OVER, etc.)
- Analizan momentum, riesgo y comportamiento temporal de activos

Implementación
CREATE INDEX idx_indicadores_tiempo
ON indicadores_tecnicos (ticker_id, fecha DESC);

## 🛠️Detalles técnicos

ticker_id
Permite localizar rápidamente todos los indicadores asociados a un activo específico.

fecha DESC
Optimiza consultas que priorizan los datos más recientes, que son las más comunes en:
- Backtesting
- Señales de trading
- Dashboards en tiempo real
- Sistemas de alertas

Casos de Uso Optimizados

Este índice acelera consultas como:
- Último RSI / SMA de un ticker
- Cálculo de cambios diarios con LAG
- Detección de divergencias técnicas
- Evaluaciones de riesgo recientes (kurtosis / skewness)
- Análisis rolling por ventana temporal

## ☑️Ejemplo típico beneficiado:

SELECT *
FROM indicadores_tecnicos
WHERE ticker_id = 'AAPL'
ORDER BY fecha DESC
LIMIT 30;

## 📉Impacto en Performance

Beneficios esperados:

🚀 Reducción significativa del tiempo de respuesta

📉 Menor uso de I/O en scans completos

🧠 Mejor planificación del optimizador SQL

⚙️ Escalabilidad para grandes volúmenes históricos

Especialmente relevante en bases de datos con:
- Miles de tickers
- Años de datos diarios
- Consultas analíticas intensivas

## 🛡️Consideraciones

- El índice incrementa ligeramente el costo de escritura (INSERT/UPDATE)
- Ideal para sistemas read-heavy (análisis > ingestión)
- Complementa otros índices en precios_diarios y eventos_corporativos

## 🌐Contexto del Proyecto

Este índice forma parte de una arquitectura analítica orientada a:
- Análisis cuantitativo avanzado
- Detección de señales técnicas
- Evaluación de riesgo y eventos
- Estudios sectoriales y comparativos

## 👤Autora
Flavia Hepp Proyecto de SQL aplicó un análisis de riesgo basado en eventos.

***
⚙️ **El edge no siempre está en el modelo… a veces está en la base de datos.**

Podés tener el mejor análisis cuantitativo del mundo…

Pero si tus queries tardan segundos (o minutos),
ya llegaste tarde.

---

📊 En este caso optimicé un sistema de análisis financiero creando índices clave:

👉 `precios_diarios (ticker_id, fecha DESC)`
👉 `indicadores_tecnicos (ticker_id, fecha DESC)`
👉 `eventos_corporativos (ticker_id, fecha, tipo_evento)`

---

💡 ¿Qué cambia con esto?

* Consultas mucho más rápidas
* Mejor acceso a datos recientes (clave en mercados)
* Menor costo computacional

---

🚨 ¿Por qué importa?

Porque en análisis financiero:

👉 El tiempo de ejecución **no es técnico… es estratégico**

* Backtesting más eficiente
* Señales en tiempo real
* Mejor capacidad de iteración

---

🧠 Insight clave:
**No gana el que tiene más datos…
gana el que puede procesarlos más rápido.**

---

🔍 Este tipo de optimización permite:

✔️ Escalar sistemas cuantitativos
✔️ Reducir latencia en análisis
✔️ Construir pipelines más robustos

---

📉 En data science aplicado a finanzas, la infraestructura también es alpha.

---

#DataEngineering #Quant #SQL #DataScience #Trading #Performance #Finanzas
