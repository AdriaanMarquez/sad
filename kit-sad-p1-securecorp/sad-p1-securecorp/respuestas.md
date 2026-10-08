**Práctica 1 de SAD · SecureCorp — Respuestas**  
**Nombre y apellidos:Adrian Marquez Rodriguez**  
   
 **Usuario:amarrod**  
Responde con tus palabras, en 1-3 líneas. En la defensa te preguntaré lo mismo en voz alta.  
**Contraseñas que has usado** (solo porque es un laboratorio; en una empresa, jamás en un fichero):  
- Tu usuario:amarrod  
- mtorres:Marta2026  
![](data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAnEAAAACCAYAAAA3pIp+AAAABmJLR0QA/wD/AP+gvaeTAAAACXBIWXMAAA7EAAAOxAGVKw4bAAAANUlEQVR4nO3OMQ2AABAAsSNBCkLfE07YGfHAiAU2QtIq6DIzW7UHAMBfnGt1V8fXEwAAXrse4eQF6VhvmPsAAAAASUVORK5CYII=)  
**1. (A1)** ¿Quién es el issuer de tu ca.crt? ¿Hasta qué fecha es válido? ¿Por qué el subject  
   
 y el issuer de la CA son iguales y los de ldap.crt no?  
**-El issuer es amarrod**  
 **  
 -Tiene de fecha 3650 dias**  
**2. (A3)** Pega el comando y el resultado de tus dos búsquedas:  
a) miembros de rrhh:  
   
 dn: cn=rrhh,ou=groups,dc=securecorp,dc=local  
 objectClass: groupOfNames  
 cn: rrhh  
 member: uid=lromero,ou=people,dc=securecorp,dc=local  
 member: uid=mtorres,ou=people,dc=securecorp,dc=local  
   
 b) cn y mail de todas las personas:  
   
 dn: uid=amarrod,ou=people,dc=securecorp,dc=local  
 cn: Adrian Marquez Rodriguez  
 mail:amarrod@securecorp.local  
   
 dn: uid=mtorres,ou=people,dc=securecorp,dc=local  
 cn: Marta Torres  
 mail:mtorres@securecorp.local  
   
 dn: uid=lromero,ou=people,dc=securecorp,dc=local  
 cn: Lucia Romero  
 mail:lromero@securecorp.local  
   
 **3. (A4)** ¿Por qué la clave `ldap.key` tiene que ser de `openldap` y tener permisos 600?  
   
 Porque el demonio de OpenLDAP (slapd) se ejecuta bajo el usuario openldap y necesita permisos de lectura  
   
 **4. (A4)** ¿Qué valor has puesto en `SLAPD_SERVICES` y por qué?  
   
 He configurado ldap:/// ldaps:/// para que el servidor escuche simultáneamente peticiones en texto plano (LDAP) y peticiones cifradas y seguras (LDAPS).  
   
 **5. (A4)** Antes de añadir `TLS_CACERT` en el cliente, `ldaps://` no funcionaba. ¿Por qué?  
   
 Porque el cliente no confiaba en el certificado del servidor al ser autofirmado, necesitaba conocer la clave pública de la CA para tener el canal seguro.  
   
 **6. (B3)** Pega la salida de `klist` con tus dos tickets. ¿Para qué sirve cada uno? ¿Ha viajado tu  
 contraseña por la red?  
   
   
Ticket cache: FILE:/tmp/krb5cc_0  
   
 Default principal: [amarrod@SECURECORP.LOCAL](mailto:amarrod@SECURECORP.LOCAL "mailto:amarrod@SECURECORP.LOCAL")  
Valid starting     Expires            Service principal  
   
 10/08/26 14:14:24  10/09/26 00:14:24  krbtgt/SECURECORP.LOCAL@SECURECORP.LOCAL  
   
 renew until 10/15/26 14:14:24  
   
 10/08/26 14:14:50  10/09/26 00:14:24 host/web.securecorp.local@SECURECORP.LOCAL  
   
 renew until 10/15/26 14:14:24  
 Uno es el TGT para autenticarse en el KDC, y el otro es el TGS para acceder al servicio específico.  
   
 No, la contraseña no viaja por la red, se usa localmente para descifrar un bloque y el KDC valida mediante cifrado Kerberos.  
   
 **7. (C)** En el `docker-compose.yml`, ¿qué diferencia hay entre `build:` e `image:`? ¿Qué  
 significa la línea `- "8081:80"` del servicio `phpldapadmin`?  
   
 Build construye una imagen localmente a partir de un Dockerfile y image descarga una imagen ya construida desde un repositorio.  
   
 Significa que redirige el puerto 8081 de tu máquina física al puerto 80 interno del contenedor de phpldapadmin.  
   
 **8. (C)** ¿Por qué en la máquina `web` no has tenido que escribir a mano `TLS_CACERT`, y en el  
 cliente sí? ¿Qué pasaría con esa línea del cliente si hicieras `./lab.sh reset`?  
   
 Porque en la máquina web el script ya sabe la ruta del certificado y el cliente no.  
   
 Si ejecutas ./lab.sh reset se borraría todas las configuraciones y se restablece el entorno  
   
