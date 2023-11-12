============================

"Firma F�cil con @firma" v1.01

===========================
==== Texto de licencia ====
===========================

Copyright (C) 2011 [Gobierno de Espana]
 This file is part of "Cliente @Firma".
 "Cliente @Firma" is free software; you can redistribute it and/or modify it under the terms of:
   - the GNU General Public License as published by the Free Software Foundation; 
     either version 2 of the License, or (at your option) any later version.
   - or The European Software License; either version 1.1 or (at your option) any later version.
 Date: 11/01/11
 You may contact the copyright holder at: soporte.afirma5@seap.minhap.es

===========================
==== Requisitos M�nimos ===
===========================

Entorno de ejecuci�n de Java 6u30 o superior.
Sistema Operativo:
-Windows XP, Vista o 7.
-Mac OS X Snow Leopard o Lion.
-Linux 2.6 o superior.

============================
== Instrucciones de carga ==
============================

En entorno gr�fico: arranque directo del fichero "SimpleAfirma.jar"
En l�nea de comandos:
	java -jar SimpleAfirma.jar
Consulte la documentaci�n de su entorno de ejecuci�n de Java y de su sistema operativo para
m�s detalle sobre la carga de aplicaciones java en JAR auto-ejecutables.

============================
=== Incidencias comunes ====
============================

Para la firma de ficheros de gran tama�o es necesario asignar una mayor cantidad de memoria al
entorno de ejecuci�n de Java. Consulte la documentaci�n de su entorno de ejecuci�n de Java.
En entornos Sun/Oracle JRE y OpenJDK puede usar la singuiente sintaxis en l�nea de comandos:
	java -Xmx2096M -jar SimpleAfirma.jar
Este comando cargar� el aplicativo permitiendo el uso de un m�ximo de 2GB de memoria. Puede
probar distintas cantidades de memoria dependiendo de la instalada en su equipo y el tama�o de
los ficheros que desee firmar

============================
=== Registro de cambios ====
============================

v1.0
-Versi�n inicial

v1.01
-Correcci�n de errores en la obtenci�n de los colores por defecto del sistema operativo.
-Correcci�n de errores en la visualizaci�n de los resultados de las firmas.
-Ahora se permite �nicamente una instancia en ejecuci�n.
-Correcci�n de errores menores.

============================