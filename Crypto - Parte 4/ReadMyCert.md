# ReadMyCert

## Descripción del Reto
Este reto de nivel medio (100 puntos) pertenece a la categoría de Criptografía y se encarga de analizar la estructura de un archivo **CSR (Certificate Signing Request)**. El objetivo es inspeccionar los metadatos de identidad encapsulados en el estándar de sintaxis PKCS#10 para extraer la bandera incrustada en el atributo del Nombre Común (*Common Name*).

## Análisis de Estructuras CSR (PKCS#10)
Una Solicitud de Firma de Certificado es un bloque de información codificado en Base64 bajo el formato PEM. Los metadatos del sujeto (*Subject*) contienen los atributos de identidad de forma estructurada. Un detalle crítico en este desafío es que la bandera presenta una alteración sintáctica deliberada en sus separadores, omitiendo el guion bajo en la sección central (`read_mycert_...`) para evadir filtros de búsqueda por diccionario comunes.

## Proceso de Reconstrucción
Se realizó la decodificación del bloque binario ASN.1 para aislar los caracteres exactos mapeados en la propiedad `CN`:

# **Flag Obtenida**: 

`picoCTF{read_mycert_57f58832}`