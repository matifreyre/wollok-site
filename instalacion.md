---
layout: hyde
title: 'Instalación'
weight: 20
lang: 'es'
---

<div class="slideLeft">
	<img src="/images/Wollok_Installation.jpg" width="100%"/>
</div>

# Entorno de Programación

Wollok está implementado dentro de la plataforma Eclipse y necesita instalar una Máquina Virtual de Java 1.8. La misma se puede descargar [aquí](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

Algunas aclaraciones:

* Tiene que ser Java **1.8** (no puede ser una versión anterior)
* Tiene que ser una **JDK** (Java Development Kit), que viene con el compilador de Java. Una JRE (Java Runtime Environment) no te va a funcionar correctamente.
* Si ya estás usando Eclipse con Java 1.8, no hace falta que la descargues otra vez.

Una vez que tengamos la VM de Java, se puede instalar Wollok descomprimiendo el contenido del archivo Zip o Tar.Gz (depende de la plataforma), en cualquier directorio. Te dejamos aquí las versiones ya empaquetadas (que solo hay que descomprimir):

* Linux: [32](http://download.uqbar.org/wollok/products/stable/wollok-linux.gtk.x86.zip) / [64 bits](http://download.uqbar.org/wollok/products/stable/wollok-linux.gtk.x86_64.zip)
* Mac [64 bits](http://download.uqbar.org/wollok/products/stable/wollok-macosx.cocoa.x86_64.zip)
* Windows [32](http://download.uqbar.org/wollok/products/stable/wollok-win32.win32.x86.zip) / [64 bits](http://download.uqbar.org/wollok/products/stable/wollok-win32.win32.x86_64.zip)

<hr> 

# Problemas comunes al instalar Wollok

Si no te aparece la opción para crear un proyecto Wollok, ni tampoco una clase, hay que revisar si el entorno Wollok está apuntando a una JDK que además sea de Java 8 ó superior. Una JDK viene con el compilador, mientras que una JRE solo trae la versión "runtime" o de ejecución de los programas Java compilados previamente (los archivos _.class_).


## Variable de entorno JAVA_HOME

A veces pese a instalar correctamente la JDK 1.8, el sistema operativo sigue utilizando por defecto otra instalación de Java, basado en la variable del entorno JAVA_HOME (y por ende, también la variable PATH). Para chequear esto, abrí una línea de comandos y revisá adónde apunta dicha variable:

```bash
$ env | grep JAVA   // Linux & Mac

> SET JAVA_HOME     // Windows
```

La podés cambiar para que apunte a tu instalación JDK 1.8, siguiendo [estos instructivos](https://docs.oracle.com/cd/E21454_01/html/821-2532/inst_cli_jdk_javahome_t.html)


## Configuración de la JDK desde Eclipse

Si en el entorno Wollok ingresás a esta configuración: Windows > Preferences > java > Installed JREs y no ves ninguna JDK o bien una JDK que no es 1.8, podés cambiarla de la siguiente manera:

* Add  > Standard VM > next 
* Elegir el directorio donde instalaron la JDK 1.8. Ej: /Library/Java/JavaVirtualMachines/jdk1.8.0_91.jdk/Contents/Home (eso dependerá del path donde lo descargaste)


## Ubuntu 16.04

Hay un [bug](https://bugs.launchpad.net/ubuntu/+source/java-common/+bug/1552764) de Eclipse en Ubuntu 16.04 que causa problemas al querer crear un proyecto. Para solucionarlo basta con agregar un par de líneas en el archivo `wollok.ini` que se encuentra en donde hayas instalado Wollok, el archivo debería quedar así:

```bash
-startup
plugins/org.eclipse.equinox.launcher_1.3.100.v20150511-1540.jar
--launcher.library
plugins/org.eclipse.equinox.launcher.gtk.linux.x86_64_1.1.300.v20150602-1417
--launcher.GTK_version
2
-vmargs
-XX:PermSize=64M
-XX:MaxPermSize=128M
```

## No levanta la aplicación (exit code 13)
Si al tratar de levantar Eclipse te aparece una pantalla de error como la siguiente:

<div class="slide">
	<img src="/images/troubleshooting/exit-code-13.png"/>
</div>

el problema puede darse porque 

* estás apuntando en el wollok.ini a una JDK inexistente (fijate qué dice el parámetro -vm)
* utilizaste la aplicación "Java Updates" en lugar de descargarlo de la página del JDK, como está documentado [en este link](http://stackoverflow.com/questions/27019786/eclipse-java-was-started-but-returned-error-code-13). En ese caso la solución es desinstalar la JDK actual, instalar la JDK según se sugiere en esta página y levantar el Wollok normalmente.


## Falta la dependencia a org.uqbar.project.wollok.launch al ejecutar un archivo

<div class="slide">
	<img src="/images/troubleshooting/wollok-launch.png" style="width: 95%"/>
</div>

Aunque el error no es muy descriptivo -y trabajaremos para mejorar eso- el problema es que estás tratando de ejecutar un test, programa o archivo Wollok que no está en el source folder del proyecto. Por defecto el source folder de cualquier proyecto Wollok es "src", así que si creás un archivo fuera de esa carpeta no te lo va a reconocer como ejecutable (esto también te puede pasar si descargás un proyecto del svn apuntando al repositorio raíz en lugar de hacerlo a la carpeta trunk). La solución es mover el archivo a la carpeta src, o cualquier otra carpeta que definas como "Source Folder".


## Me pide que instale Java 6 (solo en Mac)
En máquinas Mac aparece un extraño cartel que indica que instalemos la versión de Java 6

<div class="slide">
	<img src="/images/troubleshooting/java6.png"/>
</div>

Esto no es cierto, hay que instalar JDK 1.8. A futuro solucionaremos este tema que puede prestar a confusión.

<hr> 

# Instalación desde el Update Site

Esta opción es para aquellos usuarios avanzados que ya poseen una instalación de Eclipse y desean agregar la posibilidad de trabajar con Wollok (**no es necesario hacerlo si descargaste el entorno Wollok comprimido**).

El Update Site requiere instalarse en una instalación de JDT de Eclipse (o sea que tenga Java). Para hacer eso agregar como Software Update Site:

* [http://update.uqbar.org/wollok/stable](http://update.uqbar.org/wollok/stable) : para acceder a la última versión estable. Esta es la opción **recomendada**.
* [http://update.uqbar.org/wollok/dev](http://update.uqbar.org/wollok/dev) : si querés tener los últimos cambios en proceso (pueden aparecer errores hasta que la versión se estabilice)

<img src="/images/screencasts/Wollok-UpdateSite.gif" width="100%"/>

<hr> 

# Configuración en inglés

Si querés configurar Wollok para que levante el IDE en inglés, es necesario agregar una **nueva línea al final** del archivo de configuración `wollok.ini`, localizado en el mismo directorio donde descargaste Wollok, con la siguiente instrucción:

```bash
-Duser.language=en
```

<hr>

<div>
<img src="/images/bug.png" height="64" width="64" align="left"/>
<h1>&nbsp;&nbsp;Encontré un Bug... ¿qué hago?</h1>
</div><br>
Wollok es una pieza de Software en constante mejora y crecimiento. Como todas las cosas que están en constante evolución es probable que encuentres problemas o se te ocurra una mejora posible que te gustaría ver. 

En caso de encontrar un error, es de mucha ayuda que lo reportes en la página de GitHub de Wollok. Para eso estamos usando un [Issue Tracker](https://github.com/uqbar-project/wollok/issues) (o sea un gestor de errores / incidentes). 

Para hacerlo, algunas recomendaciones:

* Lo más importante es ponerle un título descriptivo que explique el problema lo más claramente posible, y en la descripción indicar los pasos para reproducirlo. Sin esto es muy difícil que podamos solucionar los errores.
* Verás que muchos errores están en inglés, no te sientas intimidado por eso: sentite libre de escribir en castellano si no te sentís cómodo escribiendo en inglés.
* Siempre conviene mirar primero entre los bugs existentes, si alguien no reportó antes lo mismo que estás queriendo reportar.
* Si podés, asociale alguno de estos labels:
	* *Show stopper*: si es un problema que te impide trabajar o sospechás que le va a impedir trabajar a alguien más
	* *Bug*: un error en el sistema que no impide trabajar
	* *Usability*: cuestiones que pueden confundir a los usuarios. Dado que es una herramienta pensada para personas que están dando sus primeros pasos en la programación, presentar una interfaz consistente es muy importante.
	* *Enhancement*: nuevas características que se solicitan
	* *Nice to have*: características deseadas pero menos prioritarias
	* *Question*: dudas, por ejemplo algo que no estamos seguros si es un bug

