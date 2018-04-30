## ETL EOH

**Formación ETL con Cristina Tardío (StrateBI)**

* Tenemos ETL para migración histórica y carga incremental.
* MIGRACIÓN: opt/pentaho/etl/migracion/eoh/migracion_eoh.kjb 
* INCREMENTAL: opt/pentaho/etl/01_procesamiento/EOH/EOH_procesamiento.kjb
* MaestrasEOH.xlsx --> opt/pentaho/datos
* API del INE: interpretamos los JSON que obtenemos
* 19981201 porque no está incluido, para que empieze en enero 1999
* Rangos de fechas: 19981201: (dejamos vacío el segundo término)
* tipAM --> para que traiga los metadatos
* det = 2 --> más detalle
* $.*. JSON PATH, leer el step de Pentaho "JSON INPUT"

IMPORTANTE:
Se ha dejado dos variables para cuando en el INE cambien nombre de destino, o cualquier cambio de maestras.

```
CARGA_EOH_INC_COMPLETA = 0 
CARGA_EOH_MAESTRA = 0
```

Por defecto están desactivadas, para realizar incrementales normales y no volver a cargar las dimensiones, mientras no haya cambios.

Habría que pasarlas a = 1 para activarlas. Mirar en kettle.properties
--------------------------------------------------------

**Análisis de migración_eoh.kjb**

* Trato de replicar en local
* API INE: http://www.ine.es/dyngs/DataLab/manual.html?
* JSON Path: https://github.com/json-path/JsonPath

**Análisis de EOH_Procesamiento.kjb**

* Seguir entendiendo la selección de rango_fechas: 

```sql 
SELECT 
case when ((max(anyo) || substring(max(periodo) from 2) || '01:') is null) or ${CARGA_EOH_INC_COMPLETA}='1' then '19981201:' 
else max(anyo) || substring(max(periodo) from 2) || '01:' end as rango_fechas 
FROM ${STG_SCHEMA}.mas_eoh_th
WHERE fiabilidad_dato like 'Definitivo' 
```







