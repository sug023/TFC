# ¿Qué haremos en esta fase?

En esta fase se documentará la instalación y configuración base de la estructura física necesaria para el funcionamiento del proyecto.



## Configuración de router_1

Para los routers vamos a usar la guía [0.1.0_instalacion_de_arch_linux](Guias/0.1.0_instalacion_de_arch_linux.md).

## Importación de las OVAs

Las máquinas virtuales parten de una instalación estándar de Kubuntu, sobre la que se ejecuta posteriormente un script para realizar diferentes configuraciones automáticas, como la shell, zshrc, gestor de ventanas, entre otras.

Estas configuraciones son de carácter personal y no afectan al funcionamiento del proyecto, por lo que se ha decidido omitir su documentación para evitar información innecesaria y centrarnos únicamente en las configuraciones relevantes para la infraestructura y el proyecto.
## Configuración de la máquina 1

### INstalación de xampp
Para proporcionar el entorno necesario para ejecutar la aplicación web, se utilizará **XAMPP**. Para su instalación, se accede a la página oficial de XAMPP y se descarga el instalador correspondiente para Linux, en este caso, la versión **8.2.12**.
Una vez descargado el instalador, se ejecuta desde la interfaz gráfica y se sigue el asistente de instalación, utilizando las opciones predeterminadas hasta completar el proceso.
### INstalación de WORDPRESS
Para instalar **WordPress**, se descargará el archivo comprimido correspondiente a la versión **7.1** desde su página oficial.

Una vez descargado, se descomprimirá el archivo y se copiará el directorio resultante dentro de:

```
/opt/lampp/htdocs/
```

De esta forma, WordPress quedará ubicado dentro del directorio utilizado por Apache para servir los archivos de la aplicación web.

## Configuración de la máquina 2

## Instalación de arch
Para los routers los instalare manualmente desde la línea de comandos siguiendo la siguiente documentación 