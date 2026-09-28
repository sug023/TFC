## Fase 0 — Cimientos técnicos

- [ ] Instalar y configurar entorno XAMPP
- [ ] Instalar y configurar WordPress
- [ ] Base de datos externa
- [ ] Diseñar la estructura definitiva de la base de datos (usuarios, saldo, movimientos, tipo de movimiento, relación con juegos)
- [ ] Definir la estrategia de integración de los módulos con WordPress (plugin propio / varios plugins / tema hijo)
- [ ] Configurar sistema de usuarios de WordPress como base de autenticación

## Fase 1 — Núcleo del sistema (Core)

- [ ] Sistema centralizado de saldo (comprobar, descontar, añadir)
- [ ] Sistema de movimientos (registro de toda modificación de saldo)
- [ ] Reglas de saldo: número entero, sin decimales, sin límite máximo
- [ ] Reglas de apuesta: entero, mínimo 1 §, rechazo si supera el saldo
- [ ] Mensaje de error sutil al rechazar una apuesta
- [ ] Definir interfaz común que usarán todos los juegos para apostar/pagar/consultar saldo (para no reprogramarlo en cada módulo)
- [ ] Registro (usuario, correo, contraseña, nickname)
- [ ] Validación de nickname (único, 3-16 caracteres, solo letras y números)
- [ ] Verificación de correo con código de 6 dígitos + botón de reenvío
- [ ] Asignación automática del saldo inicial al completar registro (registrado como movimiento)
- [ ] Inicio de sesión (usuario + contraseña)
- [ ] Panel inicial con "Iniciar sesión" / "Registrarse"
- [ ] Cierre de sesión (vuelta al panel inicial)
- [ ] Recuperación de contraseña por correo electrónico

## Fase 2 — Perfil y cuenta

- [ ] Página "Mi cuenta" (estructura base)
- [ ] Cambio de contraseña (contraseña actual + nueva)
- [ ] Historial de movimientos (fecha, tipo, cantidad) con paginación de 20
- [ ] Foto de perfil: subida, cambio, eliminación (vía sistema de medios de WordPress)
- [ ] Recorte automático 1:1 centrado, validación de formato (JPG/JPEG/PNG/WEBP) y tamaño (2 MB)
- [ ] Avatar predeterminado si no hay foto
- [ ] Reglas de privacidad: qué datos son públicos (foto, nickname, saldo, ranking) y qué datos nunca se muestran (usuario WP, correo, contraseña)
- [ ] Perfil público accesible mediante URL basada en el nickname

## Fase 3 — Interfaz común

- [ ] Barra de navegación superior (no fija, desaparece al hacer scroll)
- [ ] Visualización y actualización automática del saldo en la barra
- [ ] Estética base: paleta cyberpunk (azul, morado, neón, rojo), tipografía Oxanium
- [ ] Componentes visuales reutilizables (botones, campos, paneles, mensajes)
- [ ] Footer común
- [ ] Página principal con tarjetas de juegos (imagen + nombre)
- [ ] Contenedor común para juegos (cabecera con nombre, saldo, apuesta + cuadro de juego)
- [ ]  *Animación visual del cambio de saldo
- [ ] *Adaptación responsive (tablet / móvil)

## Fase 4 — Panel de administración

- [ ] Acceso independiente al panel de administración
- [ ] Listado de jugadores en formato ranking (nickname + saldo, ordenado de mayor a menor)
- [ ] Paginación de 20 jugadores por página
- [ ] Modificación de saldo por fila (campo cantidad + botón "Aplicar", sin confirmación intermedia)
- [ ] Generación automática de movimiento al modificar saldo desde admin
- [ ] Búsqueda de jugadores por nickname (coincidencia exacta, botón "Buscar")
- [ ] Configuración del saldo inicial de nuevas cuentas

## Fase 5 — Prototipado de juegos

- [ ] Prototipo visual de Dados (antes de programar su lógica definitiva)
- [ ] Prototipos visuales del resto de páginas si quedan dudas (login, registro, mi cuenta, admin)
- [ ] Definir tipos de apuesta de Dados
- [ ] Implementación de la lógica de Dados (reglas, resultados, cálculo de premio en servidor)
- [ ] Pruebas de Dados (incluye probar condiciones de carrera en el saldo)

Este es el primer juego real: aquí se valida que el "sistema común" (Fase 1) funciona bien. Los siguientes juegos deberían tardar bastante menos porque reutilizan el patrón.

## Fase 6 — Resto de juegos (mismo patrón que Dados)

- [ ] Ruleta: definir reglas → prototipo → lógica → interfaz → pruebas
- [ ] Mines: definir reglas → prototipo → lógica → interfaz → pruebas
- [ ] Slots: definir reglas → prototipo → lógica → interfaz → pruebas

## Fase 7 — Funcionalidades secundarias (aplazables)

* [ ] Ranking público (posición, foto, nickname, saldo, nº de apuestas), paginado de 20, sin filtros
- [ ] Perfil público por URL (nickname)
* [ ] Recuperación de contraseña por correo
- [ ] Animaciones de saldo
* [ ] Responsive completo (tablet / móvil)
- [ ] Contenido definitivo del footer (si no se cerró antes)

## Transversal — Seguridad

La seguridad se revisará en cada fase, no únicamente al final.

- [ ] Cálculo de resultados y premios siempre en servidor (nunca confiar en el cliente/JS)
- [ ] Operación "comprobar saldo + descontar" de forma atómica (evitar condiciones de carrera)
- [ ] Validación server-side de todos los formularios (registro, apuestas, admin)
- [ ] Límite básico de intentos en la verificación por código de 6 dígitos (rate-limit)
