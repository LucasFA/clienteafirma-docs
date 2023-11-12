
La aplicación de firma manuscrita en tableta ha sido diseñada para
agilizar el trámite de firma presencial de documentos. Esta implementada
en forma de Applet de Java y recibe como parámetros de configuración un
fichero XML.

En este fichero se deben incluir los datos necesarios para llevar a cabo
la operación de firma y el almacenamiento del documento una vez haya
sido firmado.

A continuación, se especifica cómo se debe definir los datos de los
firmantes, la ubicación del espacio de firma en la tableta, el espacio
de firma en el documento a firmar y, si fuera necesario, la firma
adicional del documento por parte de una tercera entidad, como por
ejemplo, un funcionario.

# Configuración fichero de firma

Como se ha comentado, se requiere la configuración de un fichero XML de
firma donde se especifiquen los datos del trámite. En caso de que no se
desee incluir alguno de los datos descritos, se debe dejar la etiqueta
vacía, pero en ningún caso suprimirla.

Los siguientes puntos de este documento definen los tipos de datos que
son necesarios especificar en el fichero XML:

-   Datos del código seguro de verificación (CSV).

-   Datos para el sellado de tiempo.

-   Datos del documento a firmar.

-   Datos de los firmantes.

-   Firma adicional.

## Datos del CSV

En las primeras líneas del documento XML se describe un código de
seguridad de verificación (CSV), opcional, que debe contener las
etiquetas descritas a continuación.

Estructura XML que describe un CSV para esta aplicación:

&lt;CSV&gt;

&lt;page&gt;&lt;/page&gt;

&lt;text&gt;&lt;/text&gt;

&lt;rotation&gt;&lt;/rotation&gt;

&lt;positionOnPageLowerLeftX&gt;&lt;/positionOnPageLowerLeftX&gt;

&lt;positionOnPageLowerLeftY&gt;&lt;/positionOnPageLowerLeftY&gt;

&lt;positionOnPageUpperRightX&gt;&lt;/positionOnPageUpperRightX&gt;

&lt;positionOnPageUpperRightY&gt;&lt;/positionOnPageUpperRightY&gt;

&lt;fontSize&gt;&lt;/fontSize&gt;

&lt;/CSV&gt;

### Página del CSV

*Descripción*: Indicar en un número entero la página del documento a
firmar en el que situar el código CSV.

*Etiqueta:* page.

### Texto

*Descripción:* Introducir el contenido del CSV, una secuencia de
caracteres.

*Etiqueta:* text.

### Rotación

*Descripción:* Posición en la que debe aparecer el texto; se define como
un número entero entre 0 y 360, dependiendo del grado de rotación con el
que se quiera que el código se dibuje en el documento firmado.

*Etiqueta:* rotation

### Posición

*Descripción:* Posición en la que se sitúa el CSV, es decir, las
coordenadas en las que se debe situar el texto dentro del documento.

*Etiqueta:* positionOnPageLowerLeftX, positionOnPageLowerLeftY,
positionOnPageUpperRightX, positionOnPageUpperRightY.

### Tamaño de la fuente del texto

*Descripción:* Definir el tamaño del texto que se imprime en el
documento firmado.

*Etiqueta:* fontSize.

## Datos para el sellado de tiempo

Con el objetivo de poder garantizar que el documento firmado no se ha
modificado desde el momento en el que se generó la firma se solicita a
la Autoridad de Sellado de Tiempo (TSA) que genere un sello de tiempo
con la información del documento firmado, la fecha y hora y un
certificado electrónico de confianza.

En esta sección se describen los parámetros de sellado de tiempo que
responden a la siguiente estructura XML:

&lt;tsaParams&gt;

&lt;tsaRequireCert&gt;&lt;/tsaRequireCert&gt;

&lt;tsaPolicy&gt;&lt;/tsaPolicy&gt;

&lt;tsaURL&gt;&lt;/tsaURL&gt;

&lt;tsaUsr&gt;&lt;/tsaUsr&gt;

&lt;tsaPwd&gt;&lt;/tsaPwd&gt;

&lt;extensions&gt;

&lt;extension&gt;

&lt;oid&gt;&lt;/oid&gt;

&lt;critical&gt;&lt;/critical&gt;

&lt;value&gt;&lt;/value&gt;

&lt;/extension&gt;

&lt;/extensions&gt;

&lt;tsaHashAlgorithm&gt;&lt;/tsaHashAlgorithm&gt;

&lt;sslPkcs12File&gt;&lt;/sslPkcs12File&gt;

&lt;sslPkcs12FilePassword&gt;&lt;/sslPkcs12FilePassword&gt;

&lt;/tsaParams&gt;

### Certificado de TSA

*Descripción:* Indicar con un booleano – true o false – si se requiere
el certificado de la Autoridad de Sellado de Tiempo. En caso de que no
se establezca, se considera que no se requiere certificado.

*Etiqueta:* tsaRequireCert

### Autoridad de sellado de tiempo

*Descripción:* URL de la autoridad de sello de tiempo, en caso de que no
se indique, no se añade el sello de tiempo.

*Etiqueta:* tsaURL

### Algoritmo de huella digital

*Descripción:* Algoritmo de huella digital para el cifrado de la huella.
E n caso de que no se establezca se toma por defecto el algoritmo SHA-1.

*Etiqueta:* tsaHashAlgorithm

### Política de sellado

*Descripción*: Política de sellado de tiempo, obligatoria si se define
una Autoridad de Sellado de Tiempo para la etiqueta tsaUrl.

*Etiqueta*: tsaPolicy

### Usuario de la TSA

*Descripción:* Nombre y contraseña del usuario de la TSA. Se ignora la
contraseña s i previamente no se ha establecido un nombre de usuario.

*Etiqueta:* tsaUsr, tsaPwd

### Certificado SSL cliente

*Descripción*: Se define un nombre y una contraseña para el fichero
PKCS#12 que contiene el certificado SSL cliente que pedirá la TSA al
establecer conexiones HTTPS.

*Etiqueta:* tsaSslPkcs12File, tsaSslPkcs12FilePassword

## Datos del documento a firmar

La aplicación cifra los datos biométricos de los firmantes junto con la
huella digital del documento original evitando de esta manera la réplica
de los datos en otros documentos.

Se permite almacenar los documentos firmados tanto en un servidor, como
en local, para ello es necesaria la especificación del directorio remoto
en el que almacenarlo y el directorio local. La aplicación da la
posibilidad de almacenar tanto en los dos directorios como en uno de
ellos, no obstante, es imprescindible que se defina en el XML al menos
uno de ellos.

A continuación se especifica la estructura del fichero XML en la que se
describen los datos para la recuperación y almacenamiento del documento
firmado.

&lt;retrieveUrl&gt;&lt;/retrieveUrl&gt;

&lt;saveUrl&gt;&lt;/saveUrl&gt;

&lt;saveUrlPostParam&gt;&lt;/saveUrlPostParam&gt;

&lt;saveId&gt;&lt;/saveId&gt;

&lt;saveIdPostParam&gt;&lt;/saveIdPostParam&gt;

&lt;saveDirectory&gt;&lt;/saveDirectory&gt;

&lt;signedFileName&gt;&lt;/signedFileName&gt;

&lt;writableDirectory&gt;&lt;/writableDirectory&gt;

&lt;cert&gt;&lt;/cert&gt;

&lt;showTabletButtons&gt;&lt;/showTabletButtons&gt;

### Directorio del documento

*Descripción:* Directorio desde dónde se recupera el documento original
que se desea firmar. Puede estar definido en un repositorio
(“http://direccion.com/fichero.pdf”) o como fichero local
(“file://C:\directorio\fichero.pdf”).

*Etiqueta:* retrieveURL.

### Dirección URL para guardar el documento firmado

*Descripción:* Indicar la dirección de almacenamiento del documento
firmado. Los documentos se recibirán por URL con un parámetro definido.

*Etiqueta:* saveUrl, saveUrlPostParam.

### Identificador del documento

*Descripción:* Indicar el identificador del documento, un número entero.
En caso de que no se defina será nulo e indicar una etiqueta asignada a
este identifacdor.

*Etiqueta:* saveId, saveIdPostParam.

### Directorio para guardar el documento firmado

*Descripción*: Indicar el directorio local en el que almacenar el
documento firmado.

*Etiqueta:* saveDirectory.

### Nombre del documento firmado

*Descripción:* Nombre con el que se almacena el documento firmado. Este
nombre se utiliza para guardar el documento tanto en local como en
remoto.

*Etiqueta:* signedFileName.

### Directorio para ficheros temporales

*Descripción:* Nombre del directorio donde se almacenar los logs de las
aplicación y las dll de las tabletas de captura de firma.

*Etiqueta:*writableDirectory

### Certificado

*Descripción:* Indicar el certificado de cifrado de los datos. Este
certificado debe incluirse codificado en base 64.

*Etiqueta:* cert

### Mostrar botones en la tableta de firma

*Descripción:* Indicar mediante un booleano si se desea mostrar los
botones de la tablet de firma. Estos botones permitirán al firmante
aceptar, cancelar o repetir la operación de firma. En caso de que no se
desee mostrar al firmante la botonera, al funcionario que realice el
trámite sí que le aparecerá y por tanto, debe ser éste el que realice la
acción de aceptar, repetir o cancelar.

*Etiqueta:* showTabletButtons.

<img
src="Manual para la configuración de los campos de firma para la aplicación de firma manuscrita en tableta/media/image1.png"
style="width:3.10304in;height:2.7161in" />

Figure 1 Imagen de una tableta de firma que contiene la botonera con las
acciones de firma.

## Datos de los firmantes

Los datos de los firmantes del documento se definen en este apartado.
Para cada firmante se introducen sus datos personales, la plantilla
correspondiente para cada tipo de tableta con la que se trabaje y las
posiciones que ocupa la rúbrica de la firma en el documento firmado.

Los datos de los firmantes están definidos por la etiqueta *bioSigns* y
cada firmante es descrito es por la etiqueta *bioSign*. Esta es la
estructura XML que describe los datos de los firmantes del documento:

&lt;bioSigns&gt;

&lt;bioSign&gt;

&lt;signerData&gt;

&lt;signerName&gt;&lt;/signerName&gt;

&lt;signerSurname1&gt;&lt;/signerSurname1&gt;

&lt;signerSurname2&gt;&lt;/signerSurname2&gt;

&lt;signerId&gt;&lt;/signerId&gt;

&lt;/signerData&gt;

&lt;signHeader&gt;&lt;/signHeader&gt;

&lt;signFooter&gt;&lt;/signFooter&gt;

&lt;tablet&gt;

&lt;tabletType&gt;&lt;/tabletType&gt;

&lt;htmlTemplate&gt;&lt;/htmlTemplate&gt;

> &lt;jpegTemplate&gt;&lt;/jpegTemplate&gt;

&lt;tablet&gt;

&lt;signatureArea&gt;

&lt;x&gt;&lt;/x&gt;

&lt;y&gt;&lt;/y&gt;

&lt;width&gt;&lt;/width&gt;

&lt;height&gt;&lt;/height&gt;

&lt;/signatureArea&gt;

&lt;signatureRubricPositionOnPdf&gt;

&lt;x&gt;&lt;/x&gt;

&lt;y&gt;&lt;/y&gt;

&lt;width&gt;&lt;/width&gt;

&lt;height&gt;&lt;/height&gt;

&lt;/signatureRubricPositionOnPdf&gt;

&lt;signatureRubricPageOnPdf&gt;&lt;/signatureRubricPageOnPdf&gt;

&lt;/bioSign&gt;

&lt;bioSigns&gt;

### Datos personales

*Descripción:* Indicar los datos personales del firmante, estos datos se
definen bajo la etiqueta *signerData* y debe especificarse el nombre,
primer y segundo apellido, documento de identificación (NIE/NIF) y
puesto de trabajo del firmante.

*Etiquetas:* sigenerName, signerSurname1, signerSurname2, signerId.

### Plantilla de firma

*Descripción*: La plantilla que se muestra en la pantalla de la tableta
de firma puede ser definida o bien mediante una imagen JPEG o bien por
código HTML.

Para ello es necesario crear una plantilla de uno de los dos tipos (JEPG
o HTML) para cada tableta de firma, según el modelo del dispositivo que
se conecte. Por lo tanto, cada firmante tiene asociada una plantilla de
firma para el modelo de del dispositivo con el que vaya a realizar la
operación.

La plantilla dada en el documento anexo contiene los logos de la agencia
tributaria, en caso de querer utilizar dicha plantilla es necesario
cambiar la firma por la del firmante personalizando el campo.

Este es el aspecto que muestra la tableta en la plantilla definida en el
ejemplo adjunto en el anexo:

<img
src="Manual para la configuración de los campos de firma para la aplicación de firma manuscrita en tableta/media/image2.png"
style="width:3.52424in;height:3.30184in" />

Figure 2 Imagen de una tableta de firma con una plantilla personalizada.

*Etiqueta:* tablet, tabletType, htmlTemplate, jpegTemplate.

### Área de firma

*Descripción:* Definir el área de firma de manera que quede determinada
el área de la tableta en la que el usuario tiene que firmar y que está
definida por una coordenada (x, y); punto en el que se sitúa la esquina
superior izquierda del rectángulo de firma y por las dimensiones del
área: altura y anchura.

*Etiquetas:* signature Area, x, y, width, height

### Área de firma en el documento

*Descripción:* Área en la que se sitúa la firma en el documento,
dependiendo del firmante se ubicará en diferentes coordenadas, nunca
correspondiendo dos firmas en la misma área. Se define una coordenadas
(x,y) en la que se sitúa la esquina inferior derecha de la firma, la
altura y la anchura que ocupa dicha área.

Cabe destacar que en los documentos PDF el espacio de coordenadas parte
de la esquina inferior izquierda, siendo esta (0,0).

<img
src="Manual para la configuración de los campos de firma para la aplicación de firma manuscrita en tableta/media/image3.png"
style="width:1.58355in;height:1.88568in" />

Figure 3 Coordenadas en PDF

### Página de firma

*Descripción:* Página del documento en la que aparece la firma.

*Etiqueta:* signatureRubricPageOnPdf

## Firma adicional

Los documentos que necesiten una firma adicional de una tercera entidad
o de un funcionario deben tener completados los siguientes datos de la
estructura XML:

&lt;completeWithCriptoSign&gt;&lt;/completeWithCriptoSign&gt;

&lt;completeCriptoSignExtraParams&gt;

&lt;entry&gt;

&lt;key&gt;pkcs12&lt;/key&gt;

&lt;value&gt;&lt;/value&gt;

&lt;/entry&gt;

&lt;/completeCriptoSignExtraParams&gt;

&lt;completeCriptoSignPkcs12&gt;&lt;/completeCriptoSignPkcs12&gt;

&lt;completeCriptoSignPkcs12Alias&gt;&lt;/completeCriptoSignPkcs12Alias&gt;

&lt;completeCriptoSignPkcs12Password&gt;&lt;/completeCriptoSignPkcs12Password/&gt;

La firma del funcionario puede realizarse a través del certificado
Pkcs12 que éste tenga almacenado en al almacén de claves o bien
utilizando los parámetros de firma con certificado que se definan para
el proceso de firma.

### Firma con parámetros adicionales

*Descripción:* Para una firma con certificado, se indicará con un
booleano –true, false – en la etiqueta *completeWithCriptoSign* y se
completarán los parámetros adicionales definidos en *entry.*

*El conjunto de parámetros adicionales aceptado por la aplicación para
añadir a una firma están descritos en el* [anexo](#anexo)*.*

*Etiquetas:* completeWithCriptoSign, completeCriptoSignExtraParams

### Firma con almacén PKCS12

*Descripción:* Esta aplicación permite la firma utilizando un almacén de
claves Pkcs12. Para ello, se debe rellenar las etiquetas especificando
el nombre del certificado PKCS12 almacenado en el almacén de claves, el
nombre y la contraseña de la entidad a la que pertenece el certificado.

En caso de que no se definan los tres parámetros, la firma no se
realiza.

*Etiquetas:* completeCriptoSignPkcs12, completeCriptoSignPkcs12Alias,
completeCriptoSignPkcs12Password

# Plantilla de configuración

Plantilla de configuración del fichero XML que deberá codificarse en
base 64 y definirlo en el applet de llamada a la aplicación.

&lt;?xml version=*"1.0"* encoding=*"UTF-8"* standalone=*"yes"*?&gt;

&lt;ns2:signTask xmlns:ns2=*"es.gob.afirma.crypto.handwritten"*&gt;

&lt;CSV&gt;

&lt;page&gt;&lt;/page&gt;

&lt;text&gt;&lt;/text&gt;

&lt;rotation&gt;&lt;/rotation&gt;

&lt;positionOnPageLowerLeftX&gt;&lt;/positionOnPageLowerLeftX&gt;

&lt;positionOnPageLowerLeftY&gt;&lt;/positionOnPageLowerLeftY&gt;

&lt;positionOnPageUpperRightX&gt;&lt;/positionOnPageUpperRightX&gt;

&lt;positionOnPageUpperRightY&gt;&lt;/positionOnPageUpperRightY&gt;

&lt;fontSize&gt;&lt;/fontSize&gt;

&lt;/CSV&gt;

&lt;tsaParams&gt;

&lt;tsaRequireCert&gt;&lt;/tsaRequireCert&gt;

&lt;tsaPolicy&gt;&lt;/tsaPolicy&gt;

&lt;tsaURL&gt;&lt;/tsaURL&gt;

&lt;tsaUsr&gt;&lt;/tsaUsr&gt;

&lt;tsaPwd&gt;&lt;/tsaPwd&gt;

&lt;extensions&gt;

&lt;extension&gt;

&lt;oid&gt;&lt;/oid&gt;

&lt;critical&gt;&lt;/critical&gt;

&lt;value&gt;&lt;/value&gt;

&lt;/extension&gt;

&lt;/extensions&gt;

&lt;tsaHashAlgorithm&gt;&lt;/tsaHashAlgorithm&gt;

&lt;sslPkcs12File&gt;&lt;/sslPkcs12File&gt;

&lt;sslPkcs12FilePassword&gt;&lt;/sslPkcs12FilePassword&gt;

&lt;/tsaParams&gt;

&lt;writableDirectory&gt;&lt;/writableDirectory&gt;

&lt;retrieveUrl&gt;&lt;/retrieveUrl&gt;

&lt;saveUrl&gt;&lt;/saveUrl&gt;

&lt;saveUrlPostParam&gt;&lt;/saveUrlPostParam&gt;

&lt;saveId&gt;&lt;/saveId&gt;

&lt;saveIdPostParam&gt;&lt;/saveIdPostParam&gt;

&lt;saveDirectory&gt;&lt;/saveDirectory&gt;

&lt;signedFileName&gt;&lt;/signedFileName&gt;

&lt;cert&gt;&lt;/cert&gt;

&lt;showTabletButtons&gt;&lt;/showTabletButtons&gt;

&lt;bioSigns&gt;

&lt;bioSign&gt;

&lt;signerData&gt;

&lt;signerName&gt;&lt;/signerName&gt;

&lt;signerSurname1&gt;&lt;/signerSurname1&gt;

&lt;signerSurname2&gt;&lt;/signerSurname2&gt;

&lt;signerId&gt;&lt;/signerId&gt;

&lt;/signerData&gt;

&lt;signHeader&gt;&lt;/signHeader&gt;

&lt;signFooter&gt;&lt;/signFooter&gt;

&lt;tablet&gt;

&lt;tabletType&gt;&lt;/tabletType&gt;

&lt;htmlTemplate&gt;&lt;/htmlTemplate&gt;

> &lt;jpegTemplate&gt;&lt;/jpegTemplate&gt;

&lt;tablet&gt;

&lt;signatureArea&gt;

&lt;x&gt;&lt;/x&gt;

&lt;y&gt;&lt;/y&gt;

&lt;width&gt;&lt;/width&gt;

&lt;height&gt;&lt;/height&gt;

&lt;/signatureArea&gt;

&lt;signatureRubricPositionOnPdf&gt;

&lt;x&gt;&lt;/x&gt;

&lt;y&gt;&lt;/y&gt;

&lt;width&gt;&lt;/width&gt;

&lt;height&gt;&lt;/height&gt;

&lt;/signatureRubricPositionOnPdf&gt;

&lt;signatureRubricPageOnPdf&gt;&lt;/signatureRubricPageOnPdf&gt;

&lt;/bioSign&gt;

&lt;/bioSigns&gt;

&lt;completeWithCriptoSign&gt;&lt;/completeWithCriptoSign&gt;

&lt;completeCriptoSignExtraParams&gt;

&lt;entry&gt;

&lt;key&gt;&lt;/key&gt;

&lt;value&gt;&lt;/value&gt;

&lt;/entry&gt;

&lt;/completeCriptoSignExtraParams&gt;

&lt;completeCriptoSignPkcs12&gt;&lt;/completeCriptoSignPkcs12&gt;

&lt;completeCriptoSignPkcs12Alias&gt;&lt;/completeCriptoSignPkcs12Alias&gt;

&lt;completeCriptoSignPkcs12Password&gt;&lt;/completeCriptoSignPkcs12Password/&gt;

&lt;/ns2:signTask&gt;

# Anexo

## Listado de parámetros adicionales

Valores aceptados como parámetros adicionales para las firmas PAdES:

### allowCosigningUnregisteredSignatures

Si se establece a true se permite firmar un PDF incluso si este contiene
firmas previas no registradas dentro de campos Acrobat (*AcroFields*),
condición obligatoria sin la cual es muy probable que se corrompan las
firmas previas.  
Si no se establece o se establece a o false, al intentar firmar un PDF
que contenga firmas no registradas se lanza una excepción de tipo
PdfHasUnregisteredSignaturesException.

### *includeOnlySignningCertificate*

Si se establece a true se incluye en la firma únicamente el certificado
del firmante (y no la cadena de certificación completa). Si no se
establece o se establece a o false se incluirá toda la cadena de
certificación.

### alwaysCreateRevision

Si se establece a true siempre crea una revisión del PDF incluso cuando
el documento no contiene ninguna firma previa.  
Esto requiere que los documentos de entrada cumplan estrictamente la
especificación PDF 1.7 (ISO 32000-1:2008), y puede crear
incompatibilidades con documentos PDF acordes a la especificación 1.3
creados con bibliotecas antiguas, como por ejemplo
[QPDF](http://qpdf.sourceforge.net/).  
Si se establece a false, no crea revisiones en documentos que no
contengan firmas previas y sí las crea en documentos que ya contengan
alguna firma.

### image

Imagen que se desea insertar en el PDF antes de que este sea firmado. La
imagen debe proporcionarse en formato JPEG codificado en Base64.  
SI el documento ya contiene firmas es posible que se invaliden, por lo
que conviene usarlo únicamente en documentos sin firmas previas.

### imagePage

Página donde desea insertarse la imagen indicada mediante el parámetro
image. La numeración de las páginas comienza en uno.  
Si se indica -1 como número de página se inserta la imagen en la última
página del documento. Si se indica 0 como número de página se inserta la
imagen en todas las páginas del documento. Este parámetro es
obligatorio, si no se indica una página válida no se insertará la
imagen.

### imagePositionOnPageLowerLeftX

Coordenada horizontal inferior izquierda de la posición de la imagen
(indicada mediante el parámetro image) dentro de la página.  
Es necesario indicar el resto de coordenadas de la imagen mediante los
parámetros imagePositionOnPageLowerLeftY, imagePositionOnPageUpperRightX
e imagePositionOnPageUpperRightY.  
Es necesario indicar también una página de inserción en el parámetro
imagePage.

### imagePositionOnPageLowerLeftY

Coordenada vertical inferior izquierda de la posición de la imagen
(indicada mediante el parámetro image) dentro de la página.  
Es necesario indicar el resto de coordenadas de la imagen mediante los
parámetros imagePositionOnPageLowerLeftX, imagePositionOnPageUpperRightX
e imagePositionOnPageUpperRightY.  
Es necesario indicar también una página de inserción en el parámetro
imagePage.

### imagePositionOnPageUpperRightX

Coordenada horizontal superior derecha de la posición de la imagen
(indicada mediante el parámetro image) dentro de la página.  
Es necesario indicar el resto de coordenadas de la imagen mediante los
parámetros imagePositionOnPageLowerLeftX, imagePositionOnPageLowerLeftY
e imagePositionOnPageUpperRightY.  
Es necesario indicar también una página de inserción en el parámetro
imagePage.

### imagePositionOnPageUpperRightY

Coordenada vertical superior derecha de la posición de la imagen
(indicada mediante el parámetro image) dentro de la página.  
Es necesario indicar el resto de coordenadas de la imagen mediante los
parámetros imagePositionOnPageLowerLeftX, imagePositionOnPageLowerLeftY
e imagePositionOnPageUpperRightX.  
Es necesario indicar también una página de inserción en el parámetro
imagePage.

### attach

Contenido a añadir como adjunto al PDF, en formato Base64 (el adjunto
será el binario decodificado). Este parámetro requiere que se haya
establecido también el parámetro attachFileName.

### attachFileName

Nombre de fichero para adjuntar el contenido binario indicado mediante
attach. Este parámetro requiere que se haya establecido también el
parámetro attach.

### attachDescription

Descripción del contenido binario indicado mediante attach.

### certificationLevel

Nivel de certificación de la firma PDF.  
Los valores admitidos son numéricos, correspondiendo:

-   *0* = Firma ordinaria no certificada (por defecto)

-   *1* = Firma de autor. No se permite ningún cambio posterior en el
    documento

-   *2* = Firma de autor certificada para formularios. Se permite
    únicamente el relleno posterior de los campos del formulario

-   *3* = Firma certificada. Se permite únicamente el relleno posterior
    de los campos del formulario o el añadido de firmas de aprobación

### signatureSubFilter

Nombre del sub-filtro en el diccionario PDF para indicar el tipo de la
firma. Si no se indica este parámetro por defecto se usa
adbe.pkcs7.detached (firma PAdES básica). Es posible indicar
ETSI.CAdES.detached para generar una firma PAdES-BES, si bien el hacerlo
puede causar que al añadir firmas adicionales al PDF se invaliden las ya
existentes.

### signatureField

Nombre del campo en donde insertar la firma. Si el documento PDF tiene
ya un campo de firma pre-creado es posible utilizarlo para insertar la
firma generada, referenciándolo por su nombre.  
Si se indica un nombre de campo de firma que no exista en el documento
PDF proporcionado, se generará una excepción.

### signaturePage

Página del documento PDF donde insertar la firma. Puede usarse la
constante LAST_PAGE para referirse a la última página del documento PDF
si se desconoce el número total de páginas de este.  
Este parámetro se ignora si se ha establecido valor al parámetro
signatureField, y necesita que se establezcan valores válidos a los
parámetros signaturePositionOnPageLowerLeftX,
signaturePositionOnPageLowerLeftY, signaturePositionOnPageUpperRightX y
signaturePositionOnPageUpperRightY.

### signaturePositionOnPageLowerLeftX

Coordenada horizontal inferior izquierda de la posición del recuadro
visible de la firma dentro de la página.  
Es necesario indicar el resto de coordenadas del recuadro mediante los
parámetros signaturePositionOnPageLowerLeftY,
signaturePositionOnPageUpperRightX y
signaturePositionOnPageUpperRightY.  
Si no se indica una página en el parámetro signaturePage la firma se
inserta en la última página del documento.

### signaturePositionOnPageLowerLeftY

Coordenada vertical inferior izquierda de la posición del recuadro
visible de la firma dentro de la página.  
Es necesario indicar el resto de coordenadas del recuadro mediante los
parámetros signaturePositionOnPageLowerLeftX,
signaturePositionOnPageUpperRightX y
signaturePositionOnPageUpperRightY.  
Si no se indica una página en el parámetro signaturePage la firma se
inserta en la última página del documento.

### signaturePositionOnPageUpperRightX

Coordenada horizontal superior derecha de la posición del recuadro
visible de la firma dentro de la página.  
Es necesario indicar el resto de coordenadas del recuadro mediante los
parámetros signaturePositionOnPageLowerLeftX,
signaturePositionOnPageLowerLeftY y
signaturePositionOnPageUpperRightY.  
Si no se indica una página en el parámetro signaturePage la firma se
inserta en la última página del documento.

### signaturePositionOnPageUpperRightY

Coordenada vertical superior derecha de la posición del recuadro visible
de la firma dentro de la página.  
Es necesario indicar el resto de coordenadas del recuadro mediante los
parámetros signaturePositionOnPageLowerLeftX,
signaturePositionOnPageLowerLeftY y
signaturePositionOnPageUpperRightX.  
Si no se indica una página en el parámetro signaturePage la firma se
inserta en la última página del documento.

### signatureRubricImage

> Imagen JPEG codificada en Base64 de la rúbrica de la firma manuscrita
> que se desea aparezca como firma visible en el PDF.

### layer2Text

Texto a escribir dentro de la "capa 2" de la firma visible.  
Este texto se escribe únicamente si no se ha especificado una imagen de
rúbrica, y necesita que se indique la página y la situación dónde
mostrar el recuadro de firma mediante los parámetros
signaturePositionOnPageLowerLeftX, signaturePositionOnPageLowerLeftY,
signaturePositionOnPageUpperRightX, signaturePositionOnPageUpperRightY y
signaturePage.

### layer2FontFamily

Tipo de letra a usar en el texto de la "capa 2" de la firma visible.
Este parámetro requiere que se haya establecido también el parámetro
layer2Text.  
Los valores admitidos son numéricos, correspondiendo:

-   *0* = Courier (tipo por defecto)

-   *1* = Helvética

-   *2* = Times Roman

-   *3* = Symbol

-   *4* = ZapfDingBats

### layer2FontSize

Tamaño de letra a usar en el texto de la "capa 2" de la firma visible.
Este parámetro requiere que se haya establecido también el parámetro
layer2Text.  
Los valores admitidos son numéricos (y el valor por defecto es 12).

### layer2FontStyle

Estilo del tipo de letra a usar en el texto de la "capa 2" de la firma
visible. Este parámetro requiere que se haya establecido también el
parámetro layer2Text.  
Los valores admitidos son numéricos, correspondiendo:

-   *0* = Normal (estilo por defecto)

-   *1* = Negrita

-   *2* = Cursiva

-   *3* = Negrita y cursiva

-   *4* = Subrayado

-   *8* = Tachado

Es posible combinar estilos aplicando la operación lógica *o* sobre los
valores numéricos a combinar.

### layer2FontColor

Color del texto de la "capa 2" de la firma visible. Este parámetro
requiere que se haya establecido también el parámetro layer2Text.  
Los valores admitidos son textuales (se ignora entre mayúsculas y
minúsculas), soportándose:

-   *black* = Negro (color por defecto)

-   *white* = Blanco

-   *gray* = Gris

-   *lightGray* = Gris claro

-   *darkGray* = Gris oscuro

-   *red* = Rojo

-   *pink* = Rosa

### signReason

Razón por la que se realiza la firma (este dato se añade al diccionario
PDF, y no a la propia firma).

### **signatureProductionCity** 

Ciudad en la que se realiza la firma (este dato se añade al diccionario
PDF, y no a la propia firma).

### signerContact

Contacto del firmante, usualmente una dirección de correo electrónico
(este dato se añade al diccionario PDF, y no a la propia firma).

### **policyIdentifier** 

Identificador de la política de firma. Debe ser un OID (o una URN de
tipo OID) que identifique unívocamente la política en formato ASN.1
procesable.

### policyIdentifierHash

Huella digital del documento de política de firma (normalmente del mismo
fichero en formato ASN.1 procesable). Si no se indica una huella digital
y el parámetro policyIdentifier no es una URL accesible universalmente
se usará 0, mientras que si no se indica una huella digital pero el
parámetro policyIdentifier es una URL accesible universalmente, se
descargara el fichero apuntado por la URL para calcular la huella
digital *al vuelo*.

### policyIdentifierHashAlgorithm

Algoritmo usado para el cálculo de la huella digital indicada en el
parámetro policyIdentifierHash. Es obligatorio indicarlo cuando se
proporciona una huella digital distinta de 0.

### policyQualifier

URL que apunta al documento descriptivo de la política de firma
(normalmente un documento PDF con una descripción textual).

### ownerPassword

Contraseña de apertura del PDF (contraseña del propietario) si este
estaba cifrado.  
No se soporta la firma de documentos PDF cifrados con certificados o con
algoritmo AES256.

### headLess

Evita cualquier interacción con el usuario si se establece a true, si no
se establece o se establece a false actúa normalmente (puede mostrar
diálogos, por ejemplo, para solicitar las contraseñas de los PDF
cifrados). Útil para los procesos desatendidos y por lotes.

### avoidEncryptingSignedPdfs

Si se establece a true no cifra los PDF firmados aunque el original
estuviese firmado, si no se establece o se establece a false los PDF se
cifran tras firmarse si el original lo estaba, usando la misma
contraseña y opciones que este.

### allowSigningCertifiedPdfs

Si se establece a true permite la firma o cofirma de PDF certificados
sin consultarlo al usuario, si se establece a false o cualquier otro
valor se lanza una excepción en caso de intentar firmar o cofirmar un
PDF certificado y si no se establece se mostrará un diálogo al usuario
para que confirme que desea realizar la firma a pesar de que el
resultado serán una firma no válida.  
**Si el parámetro headLess está establecido a true, no podrá mostrar el
diálogo de confirmación así que llegados a este punto se lanzará una
excepción.**  
No se soporta el cifrado de documentos PDF con certificados o con
algoritmo AES256.

### tsType

Tipo de sello de tiempo a aplicar:

-   1 = Solo sello a nivel de firma.

-   2 = Solo sello a nivel de documento.

-   3 = Dos sellos, uno a nivel de firma y otro a nivel de documento.

### tsaURL

URL de la autoridad de sello de tiempo (si no se indica no se añade
sello de tiempo).

### tsaPolicy

Política de sellado de tiempo (obligatoria si se indica tsaURL).

### tsaHashAlgorithm

Algoritmo de huella digital a usar para el sello de tiempo (si no se
establece se usa SHA-1).

### tsaRequireCert

true si se requiere el certificado de la TSA, false en caso contrario
(si no se establece se asume true).

### tsaUsr

Nombre de usuario de la TSA.

### tsaPwd

Contraseña del usuario de la TSA. Se ignora si no se ha establecido
además tsaUsr.

### tsaSslPkcs12File

Nombre del fichero PKCS#12 que contiene el certificado SSL cliente que
pedirá la TSA al establecer la coneciós HTTPS.

### tsaSslPkcs12FilePassword

Contraseña del fichero PKCS#12 que contiene el certificado SSL cliente
para las conexiones HTTPS.

### signingCertificateV2

Si se indica a true se utilizará SigningCertificateV2, si se indica
cualquier otra cosa SigningCertificateV1. Si no se indica nada, se
utilizará V1 para las firmas SHA1 y V2 para el resto.

# Ejemplo

Este documento anexo es un ejemplo de documento XML para la firma de un
documento por una entidad firmante e incluye la firma del funcionario
por medio de un certificado PKCS12 ya definido.

Ejemplo:

&lt;?xml version=*"1.0"* encoding=*"UTF-8"* standalone=*"yes"*?&gt;

&lt;ns2:signTask xmlns:ns2=*"es.gob.afirma.crypto.handwritten"*&gt;

&lt;!-- PARTE 1 --&gt;

&lt;CSV&gt;

&lt;page&gt;1&lt;/page&gt;

&lt;text&gt;CSV123812347823748946&lt;/text&gt;

&lt;rotation&gt;90&lt;/rotation&gt;

&lt;positionOnPageLowerLeftX&gt;200&lt;/positionOnPageLowerLeftX&gt;

&lt;positionOnPageLowerLeftY&gt;20&lt;/positionOnPageLowerLeftY&gt;

&lt;positionOnPageUpperRightX&gt;200&lt;/positionOnPageUpperRightX&gt;

&lt;positionOnPageUpperRightY&gt;300&lt;/positionOnPageUpperRightY&gt;

&lt;fontSize&gt;15&lt;/fontSize&gt;

&lt;text&gt;CSV-1231208&lt;/text&gt;

&lt;rotation&gt;0&lt;/rotation&gt;

&lt;positionOnPageLowerLeftX&gt;100&lt;/positionOnPageLowerLeftX&gt;

&lt;positionOnPageLowerLeftY&gt;100&lt;/positionOnPageLowerLeftY&gt;

&lt;positionOnPageUpperRightX&gt;200&lt;/positionOnPageUpperRightX&gt;

&lt;positionOnPageUpperRightY&gt;200&lt;/positionOnPageUpperRightY&gt;

&lt;fontSize&gt;15&lt;/fontSize&gt;

&lt;/CSV&gt;

&lt;!-- PARTE 2 --&gt;

&lt;tsaParams&gt;

&lt;tsaRequireCert&gt;true&lt;/tsaRequireCert&gt;

&lt;tsaPolicy&gt;4.3.2.1&lt;/tsaPolicy&gt;

&lt;tsaURL&gt;http://aeat.aeat&lt;/tsaURL&gt;

&lt;tsaUsr&gt;user&lt;/tsaUsr&gt;

&lt;tsaPwd&gt;password&lt;/tsaPwd&gt;

&lt;extensions&gt;

&lt;extension&gt;

&lt;oid&gt;1.2.3.4&lt;/oid&gt;

&lt;critical&gt;false&lt;/critical&gt;

&lt;value&gt;//o=&lt;/value&gt;

&lt;/extension&gt;

&lt;/extensions&gt;

&lt;tsaHashAlgorithm&gt;SHA-512&lt;/tsaHashAlgorithm&gt;

&lt;sslPkcs12File&gt;AAECAw==&lt;/sslPkcs12File&gt;

&lt;sslPkcs12FilePassword&gt;p12password&lt;/sslPkcs12FilePassword&gt;

&lt;/tsaParams&gt;

&lt;!-- PARTE 3 --&gt;

&lt;writableDirectory&gt;C:\Temp&lt;/writableDirectory&gt;

&lt;retrieveUrl&gt;file://C:\Temp\formulario1.pdf&lt;/retrieveUrl&gt;

&lt;saveUrl&gt;&lt;/saveUrl&gt;

&lt;saveUrlPostParam&gt;&lt;/saveUrlPostParam&gt;

&lt;saveId&gt;001&lt;/saveId&gt;

&lt;saveIdPostParam&gt;id&lt;/saveIdPostParam&gt;

&lt;saveDirectory&gt;C:\Temp&lt;/saveDirectory&gt;

&lt;writableDirectory&gt;C:\Temp&lt;/writableDirectory&gt;

&lt;retrieveUrl&gt;file://C:\Temp\formulario1.pdf&lt;/retrieveUrl&gt;

&lt;saveUrl&gt;&lt;/saveUrl&gt;

&lt;saveUrlPostParam&gt;&lt;/saveUrlPostParam&gt;

&lt;saveId&gt;004&lt;/saveId&gt;

&lt;saveIdPostParam&gt;idd&lt;/saveIdPostParam&gt;

&lt;saveDirectory&gt;C:\Temp\\/saveDirectory&gt;

&lt;signedFileName&gt;PDF firmado&lt;/signedFileName&gt;
&lt;cert&gt;MIIFnTCCBIWgAwIBAgICA+owDQYJKoZIhvcNAQEFBQAwgdoxCzAJBgNVBAYTAkVTMRIwEAYDVQQIEwlCYXJjZWxvbmExSDBGBgNVBAcMP0JhcmNlbG9uYSAoc2VlIGN1cnJlbnQgYWRkcmVzcyBhdCBodHRwczovL3d3dy5hbmYuZXMvYWRkcmVzcy8gKTEnMCUGA1UEChMeQU5GIEF1dG9yaWRhZCBkZSBDZXJ0aWZpY2FjaW9uMRcwFQYDVQQLEw5BTkYgQ2xhc2UgMSBDQTETMBEGA1UEBRMKRy02MzI4NzUxMDEWMBQGA1UEAxMNQU5GIFNlcnZlciBDQTAeFw0wNjEyMzEyMzAwMDBaFw0xNDEyMzEyMzAwMDBaMIGmMRswGQYDVQQDExJBTkYgVXN1YXJpbyBBY3Rpdm8xDDAKBgNVBCoTA0FORjEXMBUGA1UEBBMOVXN1YXJpbyBBY3Rpdm8xEjAQBgNVBAUTCTEyMzQ1Njc4WjEeMBwGCSqGSIb3DQEJARYPdGVzdEBwcnVlYmEuY29tMR8wHQYDVQQLExZDbGFzZSAyIHBlcnNvbmEgZmlzaWNhMQswCQYDVQQGEwJFUzCBnzANBgkqhkiG9w0BAQEFAAOBjQAwgYkCgYEAj2qAceOf0pyATEM0BxBK7+eGA0HEZWDZpqdhCeVvsI1AqhLWQpWNg65TGXE8ijzxGU/yS94k/34gPgIkla+p/mrDaNsVY69RcLp1hWYcL61rM//In+hXlA3qUK6as942b55YyzNsbJSQPCNgkiGuIQTo1Xfsfk4XZDi+yNSRgUMCAwEAAaOCAiEwggIdMAkGA1UdEwQCMAAwCwYDVR0PBAQDAgbAMBMGCisGAQQBgY8cFAMEBQwDQU5GMBcGCisGAQQBgY8cFAQECQwHVXN1YXJpbzAWBgorBgEEAYGPHBQFBAgMBkFjdGl2bzAZBgorBgEEAYGPHBQGBAsMCTEyMzQ1Njc4WjCBiAYDVR0gBIGAMH4wfAYKKwYBBAGBjxwDBDBuMD0GCCsGAQUFBwICMDEaL0NlcnRpZmljYWRvIGVtaXRpZG8gcGFyYSByZWFsaXphY2nzbiBkZSBwcnVlYmFzMC0GCCsGAQUFBwIBFiFodHRwczovL3d3dy5hbmYuZXMvQUMvZG9jdW1lbnRvcy8wOAYIKwYBBQUHAQEELDAqMCgGCCsGAQUFBzABhhxodHRwOi8vd3d3LmFuZi5lcy9BQy9SQy9vY3NwMDkGA1UdHwQyMDAwLqAsoCqGKGh0dHA6Ly93d3cuYW5mLmVzL0FDL1JDL0FORkFDQ0xBU0VBMS5jcmwwFwYKKwYBBAGBjxwTAQQJDAcxMjMtMzIxMDEGCisGAQQBgY8cKgYEIwwhaHR0cHM6Ly93d3cuYW5mLmVzL0FDL0FDVEFTLzU2Nzg5MBYGCSsGAQQBgY8cEwQJDAczMjEtMTIzMB0GA1UdDgQWBBSxTxAznF2uoOtMW+fJUoDN6B+rJDAfBgNVHSMEGDAWgBS+O/a0MbdzJEg5xVcTlHWqn4E/LDANBgkqhkiG9w0BAQUFAAOCAQEATQgYAOwxrMRTT2Nhx7pqiNsoGT5dJmeunAv+iU5zx/VoEXB/mx+VtyLfMea3VS9LC23404XS7pz5oPwiVPLsMPZtzOcmfacVnSdRn5J7+qOO8MB+OVlXq/QmARn+1XeBCHaTQ6AMc/pdveEoGktaXwEjTslWyRD9dGDzLp04+FndQAbVcI5xRkb4vToRnhQmloUVddhQAO8usOAIb00GJFNTq4lsyZ1qT1HplQl+ngsSD1HBxkhx10Pm3KuvCunAh4um0QnSeeiq9qWIV0UZrFlMwNRXvH9OVTqSGC4PXjw2zOi2GLUfags1decu7gcGjidlELR/WHU/6lrztfdViQ==&lt;/cert&gt;

&lt;showTabletButtons&gt;false&lt;/showTabletButtons&gt;

&lt;!-- PARTE 4 --&gt;

&lt;bioSigns&gt;

&lt;bioSign&gt;

&lt;signerData&gt;

&lt;signerName&gt;Ana&lt;/signerName&gt;

&lt;signerSurname1&gt;Pérez&lt;/signerSurname1&gt;

&lt;signerSurname2&gt;García&lt;/signerSurname2&gt;

&lt;signerId&gt;12345678Z&lt;/signerId&gt;

&lt;signerPost&gt;&lt;/signerPost&gt;

&lt;/signerData&gt;

&lt;signHeader&gt;Ejemplo de cabecera&lt;/signHeader&gt;

&lt;signFooter&gt;Ejemplo de pie de firma&lt;/signFooter&gt;

&lt;tablet&gt;

&lt;tabletType&gt;STU-430&lt;/tabletType&gt;

&lt;htmlTemplate&gt;

&lt;p style="font-weight: bold; font-size:12px; margin-left:20px;"&gt;
Firme en el recuadro y pulse aceptar:

&lt;/p&gt;

&lt;div style="margin-left:20px; margin-top:58px;" &gt;

&lt;p style="font-weight: bold; font-size:12px;"&gt;

Fdo. Ana Pérez García

&lt;/p&gt;

&lt;/div&gt;

&lt;/htmlTemplate&gt;

&lt;/tablet&gt;

&lt;signatureArea&gt;

&lt;x&gt;20&lt;/x&gt;

&lt;y&gt;50&lt;/y&gt;

&lt;width&gt;275&lt;/width&gt;

&lt;height&gt;100&lt;/height&gt;

&lt;/signatureArea&gt;

&lt;signatureRubricPositionOnPdf&gt;

&lt;x&gt;75&lt;/x&gt;

&lt;y&gt;220&lt;/y&gt;

&lt;width&gt;150&lt;/width&gt;

&lt;height&gt;55&lt;/height&gt;

&lt;/signatureRubricPositionOnPdf&gt;

&lt;signatureRubricPageOnPdf&gt;1&lt;/signatureRubricPageOnPdf&gt;

&lt;/bioSign&gt;

&lt;/bioSigns&gt;

&lt;!-- PARTE 5 --&gt;

&lt;completeWithCriptoSign&gt;true&lt;/completeWithCriptoSign&gt;

&lt;completeCriptoSignExtraParams&gt;

&lt;entry&gt;

&lt;key&gt;clave&lt;/key&gt;

&lt;value&gt;valor&lt;/value&gt;

&lt;/entry&gt;

&lt;/completeCriptoSignExtraParams&gt;

&lt;completeCriptoSignPkcs12&gt;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&lt;/completeCriptoSignPkcs12&gt;

&lt;completeCriptoSignPkcs12Alias&gt;anf usuario
activo&lt;/completeCriptoSignPkcs12Alias&gt;

&lt;completeCriptoSignPkcs12Password&gt;12341234&lt;/completeCriptoSignPkcs12Password&gt;

&lt;/ns2:signTask&gt;
