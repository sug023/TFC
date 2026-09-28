# Casino Virtual

Proyecto web desarrollado para **2º SMR**, basado en un casino virtual que utiliza una moneda ficticia y no realiza transacciones con dinero real.

El proyecto combina el desarrollo de una aplicación web con la **configuración de una infraestructura de red**, servidores, bases de datos y máquinas virtuales.

---

## Objetivo

El objetivo del proyecto es desarrollar una plataforma web de casino virtual en la que los usuarios puedan registrarse, gestionar su perfil y participar en diferentes juegos utilizando una moneda virtual.

Además del desarrollo de la aplicación, se documentará y configurará la infraestructura necesaria para ejecutar los distintos servicios que forman parte del proyecto.

> **Nota:** el sistema utiliza exclusivamente moneda virtual. No se realizan apuestas ni transacciones con dinero real.

---

## Juegos

El casino contará con diferentes juegos:

- Dados
    
- Ruleta
    
- Mines
    
- Slots
    

Los juegos se diseñarán de forma modular para facilitar la incorporación de nuevos juegos en el futuro.

---

## Usuarios

El sistema contará con diferentes funcionalidades relacionadas con la gestión de usuarios:

- Registro e inicio de sesión
    
- Verificación mediante correo electrónico
    
- Nickname único
    
- Perfiles públicos
    
- Avatares personalizados
    
- Cambio de contraseña
    
- Historial de movimientos
    
- Sistema de ranking
    

---

## Sistema de moneda

El casino utiliza una moneda virtual propia:

> **EuroDólar — `§`**

El saldo se utilizará exclusivamente dentro de la aplicación para realizar apuestas y recibir premios.

**No se utiliza dinero real.**

---

## Arquitectura del proyecto

El proyecto se divide en diferentes componentes:

```text
                    ┌─────────────────┐
                    │   Usuario / Web │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │   Servidor Web  │
                    │ Apache / PHP    │
                    └────────┬────────┘
                             │
                             ▼
                    ┌─────────────────┐
                    │    Base datos   │
                    │ MySQL / MariaDB │
                    └─────────────────┘

              Infraestructura de red
              ──────────────────────
                     │
             ┌───────┴───────┐
             ▼               ▼
         Router 1         Router 2
             │               │
           DMZ          Red interna
```

La infraestructura se implementará mediante máquinas virtuales y redes virtuales configuradas en **VirtualBox**.

La documentación de esta parte incluye la instalación y configuración de los routers, direccionamiento IP, enrutamiento, NAT, firewall y comunicación entre las diferentes redes.

---

## Tecnologías

### Aplicación web

- WordPress
    
- PHP
    
- MySQL / MariaDB
    
- Apache
    
- HTML
    
- CSS
    
- JavaScript
    

### Infraestructura

- Linux
    
- Arch Linux
    
- VirtualBox
    
- NetworkManager
    
- `iptables`
    
- Git
    
- GitHub
    

---

## Diseño

La interfaz está inspirada en la estética de **Cyberpunk 2077 / Edgerunners**, utilizando:

- Fondos oscuros
    
- Colores neón
    
- Elementos de alto contraste
    
- Tipografía **Oxanium**
    

El objetivo es mantener una estética coherente en las diferentes partes de la aplicación.

---

## Documentación

Toda la documentación técnica se encuentra dentro del directorio `Desarrollo/`.

### Estructura principal

- Estructura de red
    
- Requisitos y expectativas
    
- Estructura de software
    
- Base de datos
    
- Tecnologías
    
- TODO
    

### Fases del proyecto

La documentación del desarrollo se organiza por fases:

- Fase 0
    

Dentro de cada fase se incluyen las diferentes guías necesarias para realizar la instalación y configuración de los componentes del proyecto.

---

## Estado del proyecto

**En desarrollo.**

Actualmente el proyecto se encuentra en proceso de:

- Configuración de la infraestructura de red.
    
- Instalación y configuración de las máquinas virtuales.
    
- Configuración de los routers.
    
- Preparación de los servidores.
    
- Desarrollo progresivo de la aplicación web.
    
- Documentación de las diferentes fases del proyecto.
    

---

## Proyecto académico

Proyecto desarrollado como parte de los estudios de **2º de Sistemas Microinformáticos y Redes (SMR)** con fines exclusivamente educativos.

El proyecto se encuentra en desarrollo y tanto la infraestructura como la aplicación pueden sufrir modificaciones durante las diferentes fases de implementación.