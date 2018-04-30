
Formación Pentaho Report Designer 
==================================

- Stratebi 12/01/2018
- Comprobar que tenemos los drivers de postgres en la carpeta /lib/jdbc
- /home .pentaho/simple-jndi > default.properties (se definen ahí servidor, user, pass...) (SAETA/user=pentaho SAETA/password=stratebi!SAETA_2017)
- Como en todas las herramientas de Pentaho, se necesita JAVA y declarar variables de entorno JAVA_HOME
- Añadir DataSource: JDBC -> SAETA
- Con esta herramienta se puede navegar entre informes, porque se puede dar a los objetos comportamientos
- Importante: los parámetros se crean (query, por ejemplo distinct años) y luego se meten en las querys de consulta.
- La sintaxis de los parámetros es ${nombre_parámetro}
- Para trabajar con las consultas MDX ECTA tenemos que usar el XML donde está definido el modelo.
- Para ello lo descargamos en: Gestionar fuentes de datos -> ECTA (Analysis)
- Creamos sub-reports, arrastrando de la barra lateral (hay que seleccionar BANDED)
- Ahora vamos a DataSources y agregamos el xml descargado: OLAP -> Pentaho Analysis -> Seleccionamos XML
- Hacemos botón derecho -- convertir a tabla para que nos aparezcan las variables desplegadas
- Hacemos sub-informes para cada consulta mdx.
- Para crear totales y subtotales (o cualquier operación) usamos las funciones
- Para ir más rápido, copio y pego subinformes y edito.
- Para publicar el informe: file -> publish (10.210.209.46:8080/pentaho) user/pass


El 17/01/2018 a las 13:30, Raúl Acejo escribió:
-----------------------------------------------
Hola Cristina.
He conseguido replicar el informe de prueba que hicimos en la formación y creo que ya voy entendiendo como funciona.
He intentado meter otro parámetro para filtrar los datos de la tabla por nacionalidad, pero no funciona.
Te adjunto el informe, además lo he publicado en http://10.210.209.48:8080/pentaho/ --> public/Informes/pruebas-raul_v1
¿Le puedes echar un vistazo a ver que estoy haciendo mal?

El 17/01/2018 a las 15:47, Cristina Tardío Tomeno escribió:
-----------------------------------------------------------
Hola Raúl,
El informe tiene buena pinta y no veo ningún fallo a primera vista, buen trabajo.

Lo que sí, creo que estás utilizando la versión 7.1 de pentaho report designer. Dado que el servidor es una 6.1 y por el error que aparece en el log del servidor, seguramente sea ese el fallo. Prueba a realizarlo en la versión 6.1 y a subirlo desde ahí. El informe actual no se puede abrir directamente en la versión 6.1 del report designer, pero con los dos abiertos no debería ser difícil repetirlo. He probado añadiendo el parámetro en el informe que hicimos en la formación, tal y como está en el que me has enviado y funciona.

Si no es el caso o si te sigue fallando, lo reviso más en detalle.
Si te surge cualquier cuestión, no dudes en consultármela.

El 18/01/2018 a las 11:17, Raúl Acejo escribió:
-----------------------------------------------
Buenos días Cristina.
Efectivamente, ya he podido publicar el report, creado con PRD 6.1.
http://10.210.209.48:8080/pentaho/api/repos/%3Apublic%3AInformes%3Apruebas-raul_v2.prpt/viewer
Lo que pasa es que sólo funciona bien para Alemania, si selecciono cualquier otro país, no salen datos.
¿Te importaría echarle un vistazo?
Gracias!

Fecha: 18 ene 2018 13:13 +0100
-------------------------------
Buenos días, Raúl:

Revisándolo he visto un par de cosillas.

Para el tercer trimestre no esta parametrizado el año, habría que incluir el parámetro en la consulta MDX como en el resto de trimestres.
Para la nacionalidad, pasan dos cosas.
Por un lado,he visto que funciona alguna nacionalidad más pero hay muchas combinaciones año-país para los que no hay datos.
Por otro, algunos valores como "Canadá", no se encuentran en la dimensión(al comprobarlo en STPivot) y, aún así, aparecen en la consulta SQL. El problema es que la conexión que hay definida en el report designer es a la base de datos de preproducción y este es el pentaho de producción. Al realizar los cambios para el nuevo modelo de encuestas, los entornos de pre y pro son ligeramente distintos. Por ejemplo, en el de pre hay más países o algunas dimensiones incluyen un nivel de versión de la encuesta (nacionalidad es una de ellas). Cambiando la conexión a la base de datos de pro (10.210.209.44) debería funcionar directamente, teniendo en cuenta que para algunos valores no hay datos. Si luego quieres cambiar al entorno de pre, tendrías que cambiar las referencias a pentaho y base de datos a pre, descargando el esquema del pentaho de nuevo, ya que son ligeramente distintos. Habría que revisar también las consultas, seguramente cambie alguna.