# Script para automatizar el proceso de conciliación de saldos contables CZ8-S.

## Contexto del proyecto
Durante la gestión administrativa en el sector salud, se identificó una brecha financiera en saldos de cuentas de inventarios. El problema radica en que los ingresos por compras (registrados en los Mayores Contables) no presentaban sus respectivos ajustes de egreso, principalmente por la falta de flujo documental entre bodega y el área financiera.

## Desafío técnico
El proyecto requirió la creación de un script capaz de:
1.  **Normalizar datos no estructurados:** Extraer identificadores de bodega de descripciones manuales.
2.  **Validar partida doble:** Contrastar débitos (DEBE) vs. créditos (HABER) en miles de registros.
3.  **Trazabilidad descendente:** Partir de una inconsistencia contable para identificar el producto, lote y los egresos físicos pendientes de validación en el Kardex.

## Solución: Pipeline de auditoría
El script desarrollado en Python (Pandas) ejecuta el siguiente flujo:

1.  **Uso de expresiones regulares:** Para generar llaves relacionales (`cod_bodega`).
2.  **Detección de ingresos no ajustados :** Aplicación de *Left Join* entre asientos de ingreso y ajuste para aislar registros con valores nulos (`NaN`) en la columna de HABER.
3.  **Match de información:** Cruce de registros no conciliados con el Kardex de bodega para obtener su identidad por ID de producto y/o lote.
4.  **Generación de orden de búsqueda:** Implementación de filtrado dinámico para extraer los movimientos de egreso vinculados a los ítems en cuestión.

## Resultados
- **Automatización de hallazgos:** Reducción del tiempo de identificación de discrepancias de semanas a segundos.
- **Subsaneamiento:** Identificación y soporte para la regularización de saldos pendientes de años anteriores en un 51% ($5.6M).

_**Nota:** Los datos utilizados en este repositorio son ficticios y han sido generados únicamente con fines demostrativos de la lógica de programación. No representan información real de ninguna institución._
