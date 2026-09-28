# 1. Descripción general

El proyecto consiste en desarrollar un **casino virtual basado exclusivamente en dinero ficticio**, utilizando una moneda interna denominada **EuroDólares**, cuyo símbolo será `§`.

El sistema permitirá a los usuarios registrarse, gestionar su perfil, disponer de un saldo virtual y participar en diferentes juegos de casino.

No existirá dinero real dentro del sistema. No habrá depósitos, retiradas ni conversión de EuroDólares a dinero real.

La plataforma se desarrollará sobre **XAMPP + WordPress**, utilizando el sistema de usuarios de WordPress como base para la autenticación.

---

# 2. Objetivos del proyecto

### Objetivo principal

Crear una plataforma de casino virtual funcional, modular y escalable, con una interfaz visual inspirada en una estética **Cyberpunk / [Daemon 2.0 (Tema de KDE plasma)](https://www.reddit.com/r/unixporn/comments/1fzetme/plasma_daemon_20_a_theme_inspired_by_the_ui_of/)**.

El proyecto debe estar estructurado de manera que la incorporación de nuevos juegos no obligue a modificar constantemente el núcleo del sistema.

### Objetivos técnicos

- Utilizar WordPress para la gestión de usuarios.
    
- Mantener separadas las diferentes responsabilidades del sistema.
    
- Centralizar la gestión del saldo.
    
- Centralizar los movimientos económicos.
    
- Separar la lógica de cada juego de su representación visual.
    
- Crear componentes visuales reutilizables.
    
- Mantener una arquitectura modular.
    
- Facilitar la incorporación futura de nuevos juegos.
    
- Aplicar buenas prácticas de seguridad.
    
- Mantener el código organizado y documentado.
    
- Priorizar una implementación comprensible antes que una arquitectura innecesariamente compleja.
    

---

# 3. Moneda virtual

La moneda del casino serán los **EuroDólares** con **§** como símbolo (Moneda usada en el universo de cyberpunk).

Características:

- El saldo será siempre un número entero.
    
- No existirán decimales.
    
- No habrá límite máximo de saldo.
    
- Las apuestas serán números enteros.
    
- La apuesta mínima será de `1 §`.
    
- No habrá un límite máximo de apuesta común.
    
- El saldo inicial de los nuevos usuarios será configurable por el administrador.
    
- El saldo inicial podrá ser `0 §`.
    

---

# 4. Usuarios

Existirán únicamente dos roles:

### Administrador

Responsable de la gestión básica de jugadores y saldos. Podrá añadir o restar saldo a los jugadores.

### Jugador

Usuario normal que puede acceder al casino, gestionar su perfil y participar en los juegos.

La autenticación utilizará el sistema de usuarios de WordPress.

---

# 5. Registro

El registro utilizará:

- Usuario
    
- Correo electrónico
    
- Contraseña
    
- Nickname
    

El nickname:

- Será obligatorio.
    
- Será único.
    
- Tendrá entre **3 y 16 caracteres**.
    
- Solo podrá contener letras y números.
    
- Podrá modificarse posteriormente.
    
- Será el identificador público del jugador.
    

El correo electrónico deberá verificarse mediante un **código de 6 dígitos**.

Características establecidas:

- El código no caduca.
    
- El usuario puede introducirlo nuevamente si se equivoca.
    
- No se ha establecido un límite de intentos.
    
- Existirá un botón para **reenviar el código**.
    

Al completar el registro, el jugador recibirá automáticamente el saldo inicial configurado por el administrador.

Esta asignación quedará registrada como movimiento.

---

# 6. Inicio de sesión

El usuario iniciará sesión mediante **Usuario + contraseña**.

No se utilizará el correo electrónico como método de inicio de sesión.

La pantalla inicial mostrará:

- Iniciar sesión
    
- Registrarse
    

Ambas opciones estarán disponibles desde el mismo panel.

Después de iniciar sesión correctamente, el usuario será enviado a la página principal del casino.

Al cerrar sesión, volverá al panel inicial de acceso.

La gestión de sesión utilizará el sistema estándar de WordPress para mantener la implementación sencilla.

---

# 7. Gestión de contraseña

Desde **Mi cuenta**, el jugador podrá cambiar su contraseña.

Para realizar el cambio deberá introducir:

1. Contraseña actual.
    
2. Nueva contraseña.
    

La recuperación de contraseña mediante correo electrónico queda establecida como **objetivo secundario**.

---

# 8. Perfil del jugador

Existirá una página única denominada **Mi cuenta**.

Esta página centralizará la información y configuración del jugador.

Incluirá:

- Foto de perfil.
    
- Nickname.
    
- Cambio de contraseña.
    
- Historial de movimientos.
    

La foto de perfil será opcional.

Si el jugador no tiene fotografía, se utilizará un avatar predeterminado.

El usuario podrá:

- Subir una fotografía.
    
- Cambiarla.
    
- Eliminarla.
    

Formatos permitidos:

- JPG
    
- JPEG
    
- PNG
    
- WEBP
    

Tamaño máximo **2 MB**.

La imagen será:

- Recortada automáticamente.
    
- Formato `1:1`.
    
- Centrada automáticamente.
    
- Sin selector manual de recorte.
    

Se utilizará, siempre que sea posible, el sistema de medios de WordPress para evitar crear un sistema de almacenamiento propio.

---

# 9. Privacidad

La información pública del jugador será limitada.

Se podrán mostrar públicamente:

- Foto de perfil.
    
- Nickname.
    
- Saldo.
    
- Posición en el ranking.
    

No se mostrarán públicamente:

- Usuario de WordPress.
    
- Correo electrónico.
    
- Contraseña.
    
- Otros datos privados.
    

El perfil público accesible mediante una URL basada en el nickname queda como **objetivo secundario**.

---

# 10. Sistema de saldo

Todos los juegos utilizarán un **único saldo centralizado**.

Los juegos no gestionarán directamente el saldo de forma independiente.

La arquitectura prevista será:

```text
Jugador
   │
   ▼
Sistema central de saldo
   │
   ├── Dados
   ├── Ruleta
   ├── Mines
   └── Slots
```

Esto permitirá que todos los juegos utilicen el mismo sistema para:

- Comprobar saldo.
    
- Realizar apuestas.
    
- Añadir premios.
    
- Registrar movimientos.
    

Si un jugador intenta realizar una apuesta superior a su saldo disponible:

- La apuesta será rechazada.
    
- Se mostrará un mensaje de error sutil.
    
- No se modificará el saldo.
    

---

# 11. Movimientos

Todas las modificaciones del saldo quedarán registradas.

Ejemplos:

```text
Saldo inicial     +1.000 §
Apuesta             -100 §
Premio              +200 §
Administración      +500 §
Administración      -200 §
```

Una apuesta y su premio serán **dos movimientos independientes**.

El historial mostrará únicamente:

- Fecha.
    
- Tipo de movimiento.
    
- Cantidad.
    

No mostrará el saldo resultante después de cada movimiento.

El historial:

- No tendrá filtros.
    
- No tendrá ordenación manual.
    
- Se mostrará cronológicamente.
    
- Tendrá paginación cuando existan muchos registros.
    

---

# 12. Barra de navegación

El casino utilizará una **barra superior común**.

La barra:

- Será igual en las diferentes páginas del casino.
    
- No será fija.
    
- Desaparecerá al hacer scroll.
    
- Mostrará el saldo actual.
    
- Contendrá la navegación principal.
    

Estructura prevista:

```text
CASINO
JUEGOS ▼
CUENTA ▼
§ 1.000
SALIR
```

La estructura concreta podrá modificarse durante el diseño de la interfaz.

El saldo se actualizará automáticamente después de operaciones que modifiquen el balance.

La animación visual del cambio de saldo queda como **objetivo secundario**.

---

# 13. Página principal

Después del inicio de sesión, el jugador accederá a la página principal.

La página mostrará los módulos de juegos disponibles mediante **tarjetas**.

Cada tarjeta tendrá únicamente:

- Imagen.
    
- Nombre del juego.
    

Juegos previstos inicialmente:

1. Dados
    
2. Ruleta
    
3. Mines
    
4. Slots
    

Los juegos serán módulos independientes.

---

# 14. Arquitectura modular de juegos

Cada juego tendrá su propia carpeta y módulo.

Estructura conceptual:

```text
Juegos/
├── Dados/
├── Ruleta/
├── Mines/
└── Slots/
```

Cada módulo deberá poder contener independientemente:

- Lógica del juego.
    
- Interfaz.
    
- Recursos específicos.
    
- Configuración propia.
    

La lógica del juego deberá mantenerse lo más separada posible de la representación visual.

Por ejemplo:

```text
Juego
├── Lógica
│   ├── reglas
│   ├── resultados
│   └── premios
│
└── Interfaz
    ├── HTML
    ├── CSS
    └── JavaScript
```

El objetivo es que modificar la apariencia de un juego no implique modificar necesariamente sus reglas.

---

# 15. Interfaz común de los juegos

Todos los juegos compartirán una estructura visual exterior común.

Todo lo que esté **fuera del cuadro específico del juego** deberá reutilizarse tanto como sea posible.

Esto incluye:

- Tipografía.
    
- Colores.
    
- Botones.
    
- Campos.
    
- Navegación.
    
- Saldo.
    
- Sistema de apuestas.
    
- Mensajes.
    
- Paneles.
    
- Espaciados.
    
- Componentes visuales.
    

Cada juego tendrá un contenedor común.

Conceptualmente:

```text
┌─────────────────────────────────────┐
│ DADOS       § 1.000     APUESTA     │
├─────────────────────────────────────┤
│                                     │
│                                     │
│          CUADRO DE JUEGO            │
│                                     │
│                                     │
└─────────────────────────────────────┘
```

El interior del cuadro de juego podrá ser diferente para cada módulo.

La estructura exacta del interior se decidirá durante la fase de prototipos.

---

# 16. Juegos previstos

## Dados

Será el primer juego que se desarrollará.

Se ha establecido que podrá disponer de diferentes tipos de apuesta, pero las modalidades concretas todavía están pendientes de diseño.

Antes de implementar la lógica definitiva se realizará un **prototipo visual**.

## Ruleta

Segundo juego previsto.

Su interfaz y reglas se definirán posteriormente.

## Mines

Juego basado en una mecánica de tipo buscaminas utilizando dinero virtual.

Sus reglas se definirán posteriormente.

## Slots

Juego de máquinas tragaperras utilizando EuroDólares.

Sus reglas y funcionamiento se definirán posteriormente.

---

# 17. Prototipado

Antes de implementar completamente la lógica de cada juego se crearán **prototipos visuales**.

El proceso previsto será:

```text
Diseño
   ↓
Prototipo
   ↓
Revisión
   ↓
Implementación
   ↓
Pruebas
```

Esto permitirá definir primero la experiencia visual y posteriormente conectar la lógica real del juego.

---

# 18. Panel de administración

Existirá un panel de administración independiente del panel normal del casino.

Su objetivo será mantener una gestión sencilla de:

- Jugadores.
    
- Saldos.
    
- Saldo inicial de nuevas cuentas.
    

No tendrá funcionalidades administrativas innecesarias.

El listado de jugadores tendrá formato de ranking:

```text
POS.   NICKNAME        SALDO
1      Player01       § 5.000
2      Player02       § 3.500
3      Player03       § 1.200
```

Los jugadores estarán ordenados siempre de:

**Mayor saldo → menor saldo**

Se mostrarán:

- Nickname.
    
- Saldo.
    

No será necesario mostrar el usuario de WordPress.

---

# 19. Modificación de saldos por administración

Cada jugador aparecerá como una fila.

En la propia fila habrá un campo de cantidad y un botón `Aplicar`.

Ejemplos:

```text
Player01    § 5.000    [ 100 ]    [Aplicar]
Player02    § 3.500    [-100 ]    [Aplicar]
```

Reglas:

- `100` → añadir `100 §`.
    
- `-100` → restar `100 §`.
    
- Solo números enteros.
    
- No habrá confirmación intermedia.
    
- El cambio se aplicará directamente.
    
- La operación generará automáticamente un movimiento.
    

---

# 20. Búsqueda de jugadores

El administrador podrá buscar jugadores mediante:

```text
[ Nickname ] [ Buscar ]
```

La búsqueda:

- No será automática mientras se escribe.
    
- Requerirá pulsar `Buscar`.
    
- Utilizará coincidencia exacta del nickname.
    

Ejemplo:

```text
Buscar: sug023

→ sug023
```

No se mostrarán coincidencias como `sug024` o `suh043`.

---

# 21. Saldo inicial

El administrador podrá modificar el saldo inicial que recibirán las nuevas cuentas.

Podrá establecerse:

```text
0 §
```

o cualquier cantidad entera positiva.

Esta configuración estará dentro de la misma pantalla del panel administrativo para mantener la implementación sencilla.

---

# 22. Paginación

### Panel de administración

El listado de jugadores tendrá:

**20 jugadores por página.**

### Ranking público

El ranking público tendrá:

**20 jugadores por página.**

### Historial

El historial de movimientos también tendrá paginación cuando exista una cantidad elevada de registros.

**20 movimientos por página**

---

# 23. Ranking público

El ranking público será un **objetivo secundario**.

Cuando se implemente, estará ordenado exclusivamente por:

**Saldo actual, de mayor a menor.**

La información prevista será:

- Posición.
    
- Foto.
    
- Nickname.
    
- Saldo.
     
- Número de apuestas.


Tendrá paginación de 20 jugadores por página.

No tendrá filtros ni ordenaciones alternativas.

---

# 24. Estética

La estética general estará inspirada en:

**Cyberpunk / Daemon 2.0**

Características visuales previstas:

- Azul.
    
- Morado.
    
- Neon.
    
- Rojo.
    
- Contrastes elevados.
    
- Elementos tecnológicos.
    

Tipografía principal:

**Oxanium**

La interfaz deberá intentar reutilizar al máximo los mismos componentes visuales para evitar duplicación de código.

---

# 25. Responsive

La adaptación a:

- Ordenador.
    
- Tablet.
    
- Móvil.
    

queda establecida como **objetivo secundario**.

La primera versión priorizará la experiencia en ordenador.

---

# 26. Footer

Existirá un **footer común** en las páginas del casino.

Su contenido concreto se decidirá durante el diseño de la interfaz.

---

# 27. Arquitectura conceptual

La arquitectura general prevista será similar a:

```text
Casino
│
├── Core
│   ├── Usuarios
│   ├── Autenticación
│   ├── Saldo
│   ├── Movimientos
│   └── Sistema de juegos
│
├── Juegos
│   ├── Dados
│   ├── Ruleta
│   ├── Mines
│   └── Slots
│
├── Frontend
│   ├── Login
│   ├── Registro
│   ├── Inicio
│   ├── Mi cuenta
│   ├── Ranking
│   └── Componentes comunes
│
└── Admin
    ├── Jugadores
    └── Saldos
```

La estructura definitiva se podrá adaptar durante el desarrollo si se encuentra una solución más sencilla y mantenible.

---

# 28. Principio fundamental de arquitectura

El núcleo del proyecto deberá encargarse de las funcionalidades comunes:

```text
Usuarios
   │
   ├── Autenticación
   ├── Perfil
   ├── Saldo
   └── Movimientos
           │
           ▼
      Sistema común
           │
     ┌─────┼─────┬─────┐
     ▼     ▼     ▼     ▼
   Dados Ruleta Mines Slots
```

Los juegos no deberían implementar sistemas independientes para gestionar el dinero.

De esta manera, un futuro juego nuevo podría integrarse utilizando el sistema central sin tener que crear nuevamente:

- Gestión de usuarios.
    
- Gestión de saldo.
    
- Sistema de apuestas.
    
- Registro de movimientos.
    
- Autenticación.
    
- Componentes visuales comunes.
    

---

# 29. Prioridades del desarrollo

El desarrollo se realizará progresivamente.

### Primera fase

Diseño general y estructura visual.

### Segunda fase

Prototipos de:

- Página principal.
    
- Login.
    
- Registro.
    
- Mi cuenta.
    
- Panel de administración.
    
- Dados.
    
- Ruleta.
    
- Mines.
    
- Slots.
    

**Se irán añadiendo más fases durante el desarrollo**

# 31. Aspectos todavía pendientes

Todavía no se han definido completamente:

- Reglas concretas de Dados.
    
- Sistema de pagos de Dados.
    
- Reglas de Ruleta.
    
- Reglas de Mines.
    
- Reglas de Slots.
    
- Probabilidades y premios de los juegos.
    
- Diseño definitivo de los cuadros de juego.
    
- Contenido definitivo del footer.
    
- Algunos detalles visuales.
    
- Algunos aspectos de seguridad.
    
- Estructura definitiva de la base de datos.
    
- Estrategia exacta de integración de los módulos con WordPress.
    

Estos elementos se definirán progresivamente antes de implementarlos.

---

# 32. Criterio general del proyecto

La prioridad será conseguir una aplicación que sea:

**Sencilla de utilizar → Modular → Segura → Mantenible → Escalable**

La complejidad deberá justificarse por una necesidad real del proyecto.

Se evitará crear funcionalidades innecesarias simplemente para aumentar el número de archivos o componentes.

La arquitectura deberá permitir crecer posteriormente sin sacrificar la simplicidad de la primera versión.

---

