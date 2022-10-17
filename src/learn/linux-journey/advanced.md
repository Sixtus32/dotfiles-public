# Networking Nomad (nómada de redes)
---

## Network Sharing (Red compartida)

Por lo general, la forma de transferir datos es a través del uso compartido de archivos en la red.
Existen unos métodos que nos permiten copiar datos hacia y desde diferentes máquinas en su red. 
Una de estas herramientas para compartir archivos es el comando **scp**. 

El comando:
~~~bash
$ scp
~~~

Este comando funciona como lo hace el comando **cp**, pero le permite copiar de un host a otro host en la misma red.

**IMPORTANTE**. Funciona a través de **ssh**, por lo que todas acciones utilizan la misma autenticación y seguridad que **ssh**. También se te pedirá la **contraseña** del *host* al que pretendes enviar el archivo o directorio.

- Copiar un archivo de un *host local* a uno *remoto*.
~~~bash
$ scp myfile.txt username@remotohost.com:/remote/directory
$ scp myfile.txt sixtus@192.168.245.141:/home/marcos/
~~~
- Copiar un archivo de un *host remoto* a tu *host local*.
~~~bash
$ scp username@remotehost.com:/remote/directory/myfile.txt /local/diectory
$ scp marcos@192.457.213:/home/animals/myfile.txt /home/sixtus
~~~
- Copiar un directorio de un *host local* a uno *remoto*
~~~bash
$ scp -r mydir username@remotehost.com:/remote/directory
$ scp -r animals sixtus@192.168.245.141:/home/marcos/
~~~




## Resumen.

- Use ***scp*** para realizar copias de archivos y directorios de local a remoto e vicersa.

