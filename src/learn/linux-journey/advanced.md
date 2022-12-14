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

### rsync (remote synchronization o sincronización remota)
**Rsync** es muy similar a scp, pero tiene una gran diferencia. Rsync usa un algoritmo especial que verifica de antemano si ya existen ciertos datos que se esta por copiar NO copiarlos y llevarlos al ** host local o remoto** perdiendo el tiempo sin centrase en aquellos que no se tienen constancia de.

También verifica la integridad de un archivo que se esta copiando con sumas de verificación. Estas pequeñas optimizaciones permiten una mayor flexibilidad de transferencia de archivos y hacen que **rsync** sea ideal para la sincronización de directorios de forma remota y local, copias de seguridad de datos, grandes transferencias de datos y más.

Algunos opciones del comando rsync más comunes: 
- v	→	para las salida detallada 
- r	→	recursivo en directorios
- h	→	salida legible por humanos 
- z	→	comprimido para facilitar la transferencia, ideal para conexiones lentas.

**Forma de uso**:
- Copia sincronizado de archivos en un mismo host.
~~~bash
$ rsync -zvr /my/local/directory/one /my/local/directory/two
~~~

- Copia sincronizado de archivos locales a *host remotos*.
~~~bash
$ rsync /local/directory username@remotehost.com:/remote/direct
ory
~~~

- Copia sincronizado de archivos de *host remoto* a *host local*.
~~~bash
$ rsync username@remotehost.com:/remote/directory /local/directory
~~~

### Servidor HTTP sencillo.
Nodejs dispone de una herramienta para servir archivos a través de HTTP. La cual crea un recurso compartido de red rápido al que puedan acceder otras máquinas en su red. Cree una archivo por ejemplo **hello.js** con el siguiente contenido: 

~~~js 
const http = require('http');

const hostname = '127.0.0.1';
const port = 3000;

const server = http.createServer((req, res) => {
  res.statusCode = 200;
  res.setHeader('Content-Type', 'text/plain');
  res.end('Hello World');
});

server.listen(port, hostname, () => {
  console.log(`Server running at http://${hostname}:${port}/`);
});
~~~
Al ejecutarlo :
~~~bash
$ node hello.js
~~~

Esto configura un servidor web básico al que puede acceder a través de la dirección localhost. 
Esto se puede realizar desde python3 y node como sale en el ejemplo de distinta forma.

### NFS (Network File System)

Uno de los recursos para compartir archivos de red más estándar para Linux es NFT. Este permite a un servidor compartir directorios y archivos con uno o más clientes a través de la red.
**Su configuración se realiza así:**
~~~bash
$ sudo service nfsclient start
$ sudo mount server:/directory /mount_directory
~~~
La herramienta **automount** que en su reciente versión se le conoce como **amd** cuando un archivo es accedido desde un directorio especifico, **automount** buscara a servidor remoto el servidor remoto y lo montará automáticamente.

### Samba 
Samba es lo que llamamos las utilidades de Linux para trabajar con CIFS en Linux. Además de compatir archivos, también puede compartir recursos como impresoras.


## Resumen.

- Use ***scp*** para realizar copias de archivos y directorios de local a remoto e vicersa.
- Use ***rsync*** para realizar copias de archivos y directorios de local a remoto e vicersa para mayor rendiento y para los *backups*.


