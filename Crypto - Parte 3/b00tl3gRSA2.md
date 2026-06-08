## Descripción del Reto
El desafío plantea una falla crítica de diseño y configuración en la generación del par de claves del algoritmo RSA. La descripción del reto incluye una pregunta capciosa: *"En RSA, d es mucho más grande que e, ¿por qué no usamos d para cifrar en lugar de e?"*. 

Al examinar los parámetros expuestos por la instancia activa, se observa que el exponente de cifrado proporcionado (`e`) posee un orden de magnitud idéntico al módulo compuesto $N$. Esto confirma un escenario de **Inversión de Roles de Claves (Key Role Reversal)**, donde la clave privada pesada $d$ fue expuesta públicamente y utilizada para firmar/cifrar el texto plano original.

* **Categoría:** Cryptography
* **Dificultad:** Hard (400 puntos)
* **Vulnerabilidad:** Key Role Reversal / Small Public Exponent Attack

## 🛠️ Parámetros de la Instancia Sincronizada
* **Host Remoto:** `fickle-tempest.picoctf.net`
* **Puerto Activo:** `63638`

### Criptograma Extraído ($c$):
``
57723252919877638062171764422620556961732257998715913960847572415468279354849922328388694591576901774956375508592645938172476180961775922227451660481871923898778184052791779049738579459639870301630792376570185483265659727386931110900046432100146485085783045535459020433970481194342470550498340973033653776085


## FLAG 
`picoCTF{bad_1d3a5_3801255}`