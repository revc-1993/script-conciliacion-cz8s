# Auditoría de Integridad y Conciliación de Inventarios Críticos

## 📌 Contexto del Proyecto
Durante la gestión administrativa en el sector salud, se identificó una brecha financiera de **$5.9M USD** en activos institucionales. El problema radicaba en que los ingresos por compras (registrados en los Mayores Contables) no presentaban sus respectivos ajustes de egreso, principalmente por la falta de flujo documental entre bodega y el área financiera.

## 🚀 Desafío Técnico
El proyecto requería la creación de un motor de auditoría capaz de:
1.  **Normalizar datos no estructurados:** Extraer identificadores de bodega de descripciones manuales.
2.  **Validar la Partida Doble:** Contrastar débitos (DEBE) vs. créditos (HABER) en miles de registros.
3.  **Trazabilidad Descendente:** Partir de una inconsistencia contable para identificar el producto, lote y los egresos físicos pendientes de validación en el Kardex.

## 🛠️ Solución Implementada: Pipeline de Auditoría
El script desarrollado en Python (Pandas) ejecuta el siguiente flujo:

1.  **Parsing de Identificadores:** Uso de expresiones regulares (Regex) para generar llaves relacionales (`cod_bodega`).
2.  **Detección de Huérfanos Contables:** Aplicación de un *Left Join* entre asientos de ingreso y ajuste para aislar registros con valores nulos (`NaN`) en la columna de HABER.
3.  **Vinculación Multifuente:** Cruce de registros no conciliados con el Kardex de bodega para obtener la identidad técnica de los activos (ID Producto, Lote).
4.  **Generación de Orden de Búsqueda:** Implementación de filtrado dinámico para extraer los movimientos de egreso vinculados a los ítems críticos, facilitando la recuperación física de soportes documentales.

## 📈 Impacto y Resultados
- **Automatización de Hallazgos:** Reducción del tiempo de identificación de discrepancias de semanas a segundos.
- **Saneamiento Financiero:** Identificación y soporte para la regularización del **51%** de los saldos pendientes de años anteriores.
- **Gobernanza de Datos:** Aseguramiento de la integridad de la información para procesos de transición institucional (APIT).

## 🧰 Tecnologías Utilizadas
- **Python / Pandas:** Procesamiento y limpieza de grandes volúmenes de datos.
- **Regex:** Extracción de patrones en texto no estructurado.
- **Matplotlib/Seaborn:** Visualización de la distribución de saldos (Conciliado vs. Pendiente).
