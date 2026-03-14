# Análisis A/B Testing & ROI: Rentabilidad de Campañas Digitales

## Resumen Ejecutivo
Evaluación del rendimiento y la rentabilidad de dos campañas de marketing digital (Control vs. Test) para determinar, mediante validación estadística, si la nueva estrategia de adquisición justifica su incremento de presupuesto.

## Stack Tecnológico
* **SQL:** Extracción, limpieza y agregación de datos transaccionales.
* **Excel Avanzado:** Análisis estadístico (Prueba Z de dos proporciones, Valor P), modelado financiero y reportes de negocio.

## El Problema de Negocio
El equipo de marketing invirtió $10,000 USD adicionales en una nueva campaña ("Test") con el objetivo de generar mayor tráfico web. El propósito de este análisis es determinar matemáticamente si este aumento de tráfico se tradujo en una mejora estadísticamente significativa en la **Tasa de Conversión (CR)** frente a la campaña original ("Control").

## Reporte Ejecutivo y Resultados Estadísticos
*(Inserta aquí la captura de pantalla de tu Excel: `![Resultados del A/B Test](ab_test_results.png)`)*

## Hallazgos y Recomendación Estratégica
Tras analizar el comportamiento de más de 335,000 visitantes web, los datos revelaron lo siguiente:

1. **Caída en Eficiencia:** A pesar de generar mayor volumen de tráfico, la campaña Test registró una tasa de conversión inferior (**8.64%**) en comparación con la campaña Control (**9.83%**).
2. **Validación Estadística:** La prueba Z arrojó un Z-Score de **-11.83** y un P-Value de **< 0.001**, confirmando que la caída en el rendimiento es definitiva y no un evento producto del azar.

> **Decisión Ejecutiva:** Se recomienda **detener la campaña Test inmediatamente** para frenar la pérdida de capital. El presupuesto excedente debe ser reasignado a la campaña Control, la cual ha demostrado ser un canal de adquisición financieramente más estable y rentable.

## Código de Extracción (SQL)
Consulta estructurada para limpiar valores nulos y consolidar más de 60 líneas transaccionales en las métricas base utilizadas para la prueba estadística:

```sql
-- Extracción de métricas clave para A/B Testing
-- Se filtran valores nulos para garantizar la integridad del análisis

SELECT 
    'Control Campaign' AS Campaign_Group,
    COUNT(Date) AS Days_Run,
    SUM(Spend_USD) AS Total_Spend,
    SUM(Website_Clicks) AS Total_Visitors,
    SUM(Purchase) AS Total_Conversions
FROM control_group
WHERE Website_Clicks IS NOT NULL AND Purchase IS NOT NULL

UNION ALL

SELECT 
    'Test Campaign' AS Campaign_Group,
    COUNT(Date) AS Days_Run,
    SUM(Spend_USD) AS Total_Spend,
    SUM(Website_Clicks) AS Total_Visitors,
    SUM(Purchase) AS Total_Conversions
FROM test_group
WHERE Website_Clicks IS NOT NULL AND Purchase IS NOT NULL;
