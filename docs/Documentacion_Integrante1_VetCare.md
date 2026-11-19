# Proyecto Bimestre 1: VetCare — Documentación de Casos de Uso (Integrante 1)

**Sistema web de gestión de citas y pacientes para la clínica veterinaria “Huellitas”**

* **Asignatura:** Desarrollo de Aplicaciones Web
* **Enfoque de Ingeniería de Requisitos:** Especificación de Casos de Uso (UML 2.5) y Priorización MoSCoW.
* **Responsable de este entregable:** **Anthony (Integrante 1)** — *Arquitectura Base, CSS Global, Acceso (`CU-01`, `CU-11`) y Módulo de Propietarios (`CU-02`)*.
* **Distribución del Equipo (3 Integrantes):**
  1. **Integrante 1 (Anthony):** Visión (3.1), Casos de Uso `CU-01`, `CU-02` (4 flujos CRUD) y `CU-11` (3.2), Priorización MoSCoW (3.4), Hoja de estilos global (`css/style.css`) y 6 pantallas HTML5.
  2. **Integrante 2 (Maria):** Casos de Uso `CU-03` (4 flujos CRUD), `CU-07` y `CU-08` (3.2), Diagrama de Casos de Uso UML 2.5 (3.3), Diccionario de Datos Ficticios y 7 pantallas HTML5.
  3. **Integrante 3 (Nayia):** Casos de Uso `CU-04`, `CU-05` (3 flujos), `CU-06`, `CU-09` (4 flujos CRUD) y `CU-10` (4 flujos CRUD) (3.2), Mapa Navegacional (3.5), Validación W3C, Compilación PDF, Despliegue en GitHub Pages y 9 pantallas HTML5.
* **Fecha de entrega:** 18 de noviembre de 2026.

---

## 3.1. Visión

### Planteamiento del problema
La clínica veterinaria “Huellitas”, ubicada en la ciudad de Quito, atiende un promedio de 40 mascotas al día con un equipo operativo conformado por tres médicos veterinarios, una recepcionista y un administrador. Actualmente, la totalidad de los procesos transaccionales y clínicos se ejecuta de manera manual: las citas médicas se toman por teléfono y se anotan en un cuaderno físico; los datos personales y de contacto de los propietarios se escriben a mano; y el historial clínico de cada paciente se archiva en fichas de papel dispersas.

#### ¿A quién afecta y cuál es su impacto operativo?
* **A la Recepcionista:** Sufre sobrecarga operativa al buscar fichas en papel, registra involuntariamente números de contacto incompletos o ilegibles, duplica registros de mascotas y asigna citas superpuestas en el mismo horario.
* **A los Veterinarios:** Atienden mascotas sin conocer sus atenciones anteriores (alergias, evolución de peso, diagnósticos y tratamientos previos), poniendo en riesgo la precisión clínica y retrasando la agenda diaria.
* **A los Propietarios y Mascotas:** Experimentan esperas prolongadas por cruces de turnos, pérdida de seguimiento médico y falta de comunicación oportuna.
* **A la Administración:** Carece de un catálogo centralizado y validado con los precios oficiales de los servicios veterinarios y el personal médico activo.

### Interesados y usuarios

| Interesado / Usuario | Qué necesita del sistema (Objetivos) | Responsabilidad en VetCare |
| :--- | :--- | :--- |
| **Recepcionista** (Usuario Operativo) | Registrar y buscar rápidamente propietarios y mascotas sin errores de formato; agendar, reprogramar y cancelar citas evitando cruces de horario. | Ejecutar los módulos CRUD de Propietarios (CU-02), Mascotas (CU-03), Agendar cita (CU-04) y Gestionar citas (CU-05). |
| **Veterinario** (Usuario Clínico) | Consultar de inmediato sus citas programadas para una fecha, revisar las atenciones previas del paciente y registrar diagnóstico, tratamiento y peso. | Ejecutar Consultar agenda del día (CU-06), Registrar atención médica (CU-07) y Consultar historial clínico (CU-08). |
| **Administrador** (Usuario de Gestión) | Mantener actualizado el directorio de médicos veterinarios y el catálogo de servicios con sus precios oficiales. | Ejecutar los módulos CRUD de Gestionar veterinarios (CU-09) y Gestionar servicios (CU-10). |
| **Propietario de Mascota** (Beneficiario Indirecto) | Ser atendido puntualmente sin pérdida del expediente clínico de su mascota ni errores en sus datos de contacto. | Suministrar información veraz de identificación, contacto y datos de su mascota en la recepción. |
| **Gerencia Clínica “Huellitas”** (Dirección) | Estandarizar el flujo de atención y asegurar la calidad de los datos desde el formulario de entrada. | Definir reglas de negocio, priorizar casos de uso y validar el cumplimiento de las restricciones del sistema. |

### Objetivo del sistema
Construir **VetCare**, un sistema web transaccional estático e intuitivo desarrollado con HTML5 semántico y CSS3 puro que centralice y valide desde el formulario las operaciones CRUD de propietarios, mascotas, citas, atenciones médicas, veterinarios y servicios de la clínica veterinaria “Huellitas”, para erradicar los registros manuales en papel.

### Alcance

#### ¿Qué incluye esta versión?
* **Módulo de Acceso (`CU-01`, `CU-11`):** Inicio de sesión con validación de correo y contraseña, panel de recepción y cierre de sesión.
* **Módulo CRUD de Propietarios (`CU-02`):** Listado con buscador (`type="search"`), registro validado (cédula de 10 dígitos, celular `09XXXXXXXX`, nombres solo letras), edición precargada y confirmación de eliminación.
* **Módulo CRUD de Mascotas (`CU-03`):** Registro, consulta, edición y baja de mascotas asociadas a un propietario existente, validando especie, raza (`datalist`), sexo, fecha de nacimiento no futura y peso (0.1 a 120 kg).
* **Módulo Transaccional de Citas (`CU-04`, `CU-05`):** Agendamiento de citas (lunes a sábado, 08:00 a 18:00, bloques de 30 minutos), consulta, reprogramación y cancelación con motivo obligatorio (máx. 200 caracteres).
* **Módulo Clínico y Agenda (`CU-06`, `CU-07`, `CU-08`):** Agenda diaria del veterinario, registro de atención médica (diagnóstico, tratamiento, peso y paso a estado *Atendida*) y consulta de historial clínico más detalle.
* **Módulo Administrativo (`CU-09`, `CU-10`):** Gestión CRUD del personal veterinario y del catálogo de servicios con precios entre \$1,00 y \$500,00.

#### ¿Qué queda fuera de esta versión (Out-of-Scope)?
* Procesamiento en servidor (backend) y persistencia en motor de base de datos relacional.
* Pagos en línea, pasarelas de cobro con tarjeta o facturación electrónica.
* Notificaciones automáticas por correo electrónico, SMS o WhatsApp.
* Control de inventario de farmacia/bodega y hospitalización continua.

### Características principales
* **F-01. Autenticación y Enrutamiento por Rol:** Acceso mediante correo y contraseña hacia los menús de Recepcionista, Veterinario y Administrador.
* **F-02. Gestión Validada de Propietarios (CRUD):** Control de formato en tiempo de captura para cédula ecuatoriana (10 dígitos), celular (`09XXXXXXXX`) y correo.
* **F-03. Gestión Clínica de Mascotas por Propietario (CRUD):** Asociación obligatoria a un propietario único, selección de especie y autocompletado de razas con `datalist`.
* **F-04. Agendamiento Transaccional de Citas:** Reserva de turnos médicos de lunes a sábado (08:00–18:00 en intervalos de 30 minutos) sin permitir fechas pasadas.
* **F-05. Control de Estados, Reprogramación y Cancelación de Citas:** Seguimiento de estados (*Programada*, *Atendida*, *Cancelada*) con motivo obligatorio al cancelar.
* **F-06. Consulta de Agenda Diaria del Veterinario:** Visualización ordenada por fecha y hora de los pacientes citados para cada profesional médico.
* **F-07. Registro Clínico de Atención Médica:** Documentación de diagnóstico, tratamiento y peso actualizado de la mascota, marcando la cita como *Atendida*.
* **F-08. Expediente e Historial Clínico por Paciente:** Consulta cronológica y vista detallada de todas las atenciones anteriores de una mascota.
* **F-09. Administración de Personal Veterinario (CRUD):** Registro, consulta, edición y baja de los médicos veterinarios y sus especialidades.
* **F-10. Catálogo Tarifario de Servicios (CRUD):** Administración de servicios médicos con nombre único y precio regulado entre \$1,00 y \$500,00.

### Restricciones y supuestos
* **Restricciones Tecnológicas:** Uso exclusivo de HTML5 semántico (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`) y CSS/CSS3 externo (`css/style.css`). Prohibido usar JavaScript, estilos en línea (`style="..."`) o frameworks CSS (Bootstrap, Tailwind).
* **Restricciones de Navegadores y Estándares:** Visualización y validación idénticas en Google Chrome y Mozilla Firefox; aprobación sin errores en los validadores de la W3C (HTML y CSS); contraste de color mínimo nivel AA de WCAG.
* **Restricciones de Negocio:** Cédula de 10 dígitos numéricos; celular de 10 dígitos que inicia en `09`; nombres/apellidos solo letras y espacios (2–50 caracteres); peso de mascota entre 0,1 y 120 kg con un decimal; citas de lunes a sábado de 08:00 a 18:00 cada 30 min; servicios entre \$1,00 y \$500,00.
* **Supuestos:** Todo el equipo utiliza un Diccionario de Datos Ficticios Oficial para garantizar coherencia en las 22 pantallas estáticas, con los cuatro registros oficiales del directorio de propietarios y sus mascotas asociadas: **Juan Carlos Pérez Morales** (C.I. `1712345678`, mascota `Toby`), **Pedro Andrés Vaca** (C.I. `1714567890`, mascota `Rocky`), **Ana Lucía Torres** (C.I. `1713456789`, mascota `Luna`) y **María Fernanda Salazar** (C.I. `1718765432`, mascota `Michi`).

### Glosario
* **Agenda del Día:** Listado cronológico de las citas *Programadas* asignadas a un médico veterinario para una fecha específica.
* **Atención Médica:** Consulta clínica en la que el veterinario registra diagnóstico, tratamiento y peso en kg del paciente, cambiando la cita a *Atendida*.
* **Cita Médica:** Turno reservado en una fecha y bloque de 30 minutos que asocia una mascota, un servicio veterinario y un médico veterinario.
* **Estado de la Cita:** Situación operativa de la cita: *Programada* (pendiente), *Atendida* (consulta realizada) o *Cancelada* (anulada con motivo de hasta 200 caracteres).
* **Historial Clínico:** Conjunto histórico de todas las atenciones médicas previas recibidas por una mascota dentro de la clínica “Huellitas”.
* **Mascota (Paciente):** Animal doméstico (Perro, Gato, Ave, Roedor u Otro) asociado a un único propietario y sujeto de atención veterinaria.
* **Propietario:** Persona responsable de una o más mascotas atendidas en la clínica, identificada de forma única por su cédula de 10 dígitos.
* **Servicio Veterinario:** Prestación médica o clínica ofrecida por la veterinaria con un nombre único y un precio establecido entre \$1,00 y \$500,00.

---

## 3.2. Descripción de casos de uso (requisitos)

### Catálogo general de casos de uso del sistema

| ID | Caso de uso | Actor | Descripción breve |
| :--- | :--- | :--- | :--- |
| **CU-01** | Iniciar sesión | Todos | El usuario ingresa con correo y contraseña y accede al menú de su rol. |
| **CU-02** | Gestionar propietarios | Recepcionista | Registrar, buscar, editar y eliminar propietarios. |
| **CU-03** | Gestionar mascotas | Recepcionista | Registrar, buscar, editar y eliminar mascotas asociadas a un propietario. |
| **CU-04** | Agendar cita | Recepcionista | Crear una cita para una mascota con servicio, veterinario, fecha y hora. |
| **CU-05** | Gestionar citas | Recepcionista | Consultar, reprogramar y cancelar citas existentes. |
| **CU-06** | Consultar agenda del día | Veterinario | Ver las citas programadas del veterinario para una fecha. |
| **CU-07** | Registrar atención médica | Veterinario | Registrar diagnóstico, tratamiento y peso; la cita pasa a Atendida. |
| **CU-08** | Consultar historial clínico | Veterinario | Ver las atenciones anteriores de una mascota. |
| **CU-09** | Gestionar veterinarios | Administrador | Registrar, consultar, editar y eliminar veterinarios. |
| **CU-10** | Gestionar servicios | Administrador | Registrar, consultar, editar y eliminar servicios y sus precios. |
| **CU-11** | Consultar panel de recepción | Recepcionista | Visualizar el panel principal de recepción con el resumen del día, acceder a los módulos operativos o salir de la sesión. |

---

### Especificación de casos de uso del Integrante 1 (`CU-01`, `CU-02` y `CU-11`)

#### 1. `CU-01 Iniciar sesión`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-01 Iniciar sesión** |
| **Actor** | Todos (Recepcionista, Veterinario, Administrador) |
| **Descripción** | Permite al usuario ingresar con su correo electrónico, contraseña y rol para acceder al menú correspondiente a sus funciones. |
| **Precondiciones** | El usuario se encuentra en la pantalla de inicio de sesión (`index.html`). |
| **Flujo básico** | 1. El usuario accede a la pantalla de inicio de sesión.<br>2. El sistema muestra el formulario con los campos de correo electrónico, contraseña, selector de rol y casilla para recordar sesión.<br>3. El usuario completa sus credenciales, selecciona su rol y pulsa el botón “Ingresar al Sistema”.<br>4. El sistema valida los datos y redirige al menú principal correspondiente al rol. |
| **Flujos alternos** | 3a. Un dato no cumple la validación (correo inválido, contraseña menor a 6 caracteres o rol vacío): el sistema marca el campo en rojo, muestra el mensaje y no envía el formulario.<br>3b. El usuario pulsa el botón “Limpiar”: el sistema vacía los campos del formulario.<br>3c. El usuario selecciona un enlace de acceso demostrativo por rol (Recepcionista, Veterinario o Administrador): el sistema abre directamente el panel de ese rol. |
| **Postcondiciones** | El usuario accede al menú principal de su rol dentro del sistema. |
| **Reglas y validaciones** | Correo electrónico: email, required, maxlength="80", placeholder="usuario@huellitas.ec", autocomplete="email", title con el formato.<br>Contraseña: password, required, minlength="6", maxlength="30", autocomplete="current-password", title con el formato.<br>Rol del usuario: select, required (Recepcionista, Veterinario, Administrador).<br>Mantener sesión activa: checkbox, opcional. |
| **Pantallas** | index.html, menu-recepcion.html, agenda-veterinario.html, veterinarios-listado.html |

---

#### 2. `CU-02 Gestionar propietarios — flujo Registrar propietario`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-02 Gestionar propietarios — flujo Registrar propietario** |
| **Actor** | Recepcionista |
| **Descripción** | Permite registrar un nuevo propietario de mascota validando sus datos de identificación y contacto. |
| **Precondiciones** | La recepcionista inició sesión (CU-01). |
| **Flujo básico** | 1. La recepcionista selecciona “Propietarios” en el menú.<br>2. El sistema muestra el listado de propietarios.<br>3. La recepcionista pulsa el botón “Nuevo propietario”.<br>4. El sistema muestra el formulario vacío de registro.<br>5. La recepcionista completa los datos y pulsa el botón “Guardar”.<br>6. El sistema valida los datos y vuelve al listado con el propietario registrado. |
| **Flujos alternos** | 5a. Un dato no cumple la validación (cédula distinta de 10 dígitos, celular que no inicia con 09, nombres o apellidos con números o correo inválido): el sistema marca el campo en rojo, muestra el mensaje y no envía el formulario.<br>5b. La recepcionista pulsa el botón “Limpiar”: el sistema vacía los controles del formulario.<br>5c. La recepcionista pulsa el botón “Cancelar”: el sistema regresa al listado sin guardar. |
| **Postcondiciones** | El propietario queda registrado y disponible para asociarle mascotas (CU-03). |
| **Reglas y validaciones** | Cédula: text, required, pattern="[0-9]{10}", minlength="10", maxlength="10", title con el formato.<br>Nombres: text, required, pattern="[A-Za-zÁÉÍÓÚáéíóúÑñ ]{2,50}", minlength="2", maxlength="50", autocomplete="given-name", title con el formato.<br>Apellidos: text, required, pattern="[A-Za-zÁÉÍÓÚáéíóúÑñ ]{2,50}", minlength="2", maxlength="50", autocomplete="family-name", title con el formato.<br>Teléfono celular: tel, required, pattern="09[0-9]{8}", minlength="10", maxlength="10", autocomplete="tel", title con el formato.<br>Correo electrónico: email, required, maxlength="80", autocomplete="email", title con el formato.<br>Sector en Quito: text con datalist de sectores comunes, required, minlength="3", maxlength="50".<br>Dirección domiciliaria: textarea, required, minlength="5", maxlength="150". |
| **Pantallas** | propietarios-listado.html, propietarios-nuevo.html |

---

#### 3. `CU-02 Gestionar propietarios — flujo Consultar y buscar propietario`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-02 Gestionar propietarios — flujo Consultar y buscar propietario** |
| **Actor** | Recepcionista |
| **Descripción** | Permite visualizar el listado de propietarios registrados y filtrar registros por cédula, nombre, apellido o celular. |
| **Precondiciones** | La recepcionista inició sesión (CU-01). |
| **Flujo básico** | 1. La recepcionista selecciona “Propietarios” en el menú.<br>2. El sistema muestra una tabla con cédula, nombres, apellidos, celular, correo, dirección, mascotas asociadas y acciones de cada propietario.<br>3. La recepcionista escribe un criterio en el buscador y pulsa “Buscar”.<br>4. El sistema muestra los propietarios que coinciden, con los enlaces “Editar” y “Eliminar” en cada fila. |
| **Flujos alternos** | 4a. No existen coincidencias con el término buscado: el sistema muestra el mensaje “No se encontraron propietarios”.<br>4b. La recepcionista pulsa sobre la mascota asociada: el sistema abre el listado de mascotas (CU-03). |
| **Postcondiciones** | La recepcionista visualiza la información actualizada de los propietarios registrados. |
| **Reglas y validaciones** | Buscador: search, maxlength="50", placeholder descriptivo.<br>Tabla accesible con caption, thead, tbody y th scope. |
| **Pantallas** | propietarios-listado.html |

---

#### 4. `CU-02 Gestionar propietarios — flujo Editar propietario`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-02 Gestionar propietarios — flujo Editar propietario** |
| **Actor** | Recepcionista |
| **Descripción** | Permite modificar los datos personales, teléfono, correo o dirección de un propietario existente. |
| **Precondiciones** | La recepcionista inició sesión (CU-01). El propietario existe en el listado. |
| **Flujo básico** | 1. En el listado de propietarios, la recepcionista pulsa “Editar” en la fila del propietario.<br>2. El sistema muestra el formulario precargado con los datos actuales del propietario.<br>3. La recepcionista modifica los campos requeridos y pulsa “Guardar cambios”.<br>4. El sistema valida los datos y regresa al listado con la información actualizada. |
| **Flujos alternos** | 3a. Un dato no cumple la validación: el sistema marca el campo en rojo, muestra el mensaje y no envía el formulario.<br>3b. La recepcionista pulsa “Cancelar”: el sistema regresa al listado sin aplicar cambios. |
| **Postcondiciones** | Los datos del propietario quedan actualizados en el sistema. |
| **Reglas y validaciones** | Cédula: text, required, readonly, pattern="[0-9]{10}", minlength="10", maxlength="10" (precargado con value).<br>Nombres: text, required, pattern="[A-Za-zÁÉÍÓÚáéíóúÑñ ]{2,50}", minlength="2", maxlength="50" (precargado con value).<br>Apellidos: text, required, pattern="[A-Za-zÁÉÍÓÚáéíóúÑñ ]{2,50}", minlength="2", maxlength="50" (precargado con value).<br>Teléfono celular: tel, required, pattern="09[0-9]{8}", minlength="10", maxlength="10" (precargado con value).<br>Correo electrónico: email, required, maxlength="80" (precargado con value).<br>Sector en Quito: text con datalist, required (precargado con value).<br>Dirección domiciliaria: textarea, required, minlength="5", maxlength="150" (precargado). |
| **Pantallas** | propietarios-listado.html, propietarios-editar.html |

---

#### 5. `CU-02 Gestionar propietarios — flujo Eliminar propietario`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-02 Gestionar propietarios — flujo Eliminar propietario** |
| **Actor** | Recepcionista |
| **Descripción** | Permite eliminar el registro de un propietario previa confirmación explícita. |
| **Precondiciones** | La recepcionista inició sesión (CU-01). El propietario existe en el listado. |
| **Flujo básico** | 1. En el listado de propietarios, la recepcionista pulsa “Eliminar” sobre un registro.<br>2. El sistema muestra la pantalla de confirmación con los datos del propietario a eliminar.<br>3. La recepcionista marca la casilla de confirmación y pulsa el botón “Confirmar”.<br>4. El sistema elimina el registro y regresa al listado de propietarios. |
| **Flujos alternos** | 2a. El propietario tiene mascotas con citas Programadas: el sistema muestra una advertencia indicando que deben gestionarse antes de eliminarlo.<br>3a. La casilla de confirmación no está marcada: el sistema marca el campo en rojo, muestra el mensaje y no envía el formulario.<br>3b. La recepcionista pulsa “Cancelar”: el sistema regresa al listado sin eliminar el registro. |
| **Postcondiciones** | El registro del propietario queda eliminado del listado. |
| **Reglas y validaciones** | Vista de confirmación de solo lectura con los datos del propietario.<br>Confirmación: checkbox, required (“Confirmo que deseo eliminar el registro de este propietario”).<br>Botones “Confirmar” y “Cancelar”. |
| **Pantallas** | propietarios-listado.html, propietarios-eliminar.html |

---

#### 6. `CU-11 Consultar panel de recepción`

| Campo | Especificación |
| :--- | :--- |
| **ID y nombre** | **CU-11 Consultar panel de recepción** |
| **Actor** | Recepcionista |
| **Descripción** | Permite a la recepcionista visualizar el panel principal de recepción con el resumen operativo del día y los accesos directos a los módulos de trabajo. |
| **Precondiciones** | La recepcionista inició sesión (CU-01). |
| **Flujo básico** | 1. Tras iniciar sesión como recepcionista, el sistema muestra el panel de recepción con el resumen operativo del día (“Hoy en Huellitas”) y los accesos rápidos.<br>2. La recepcionista consulta los indicadores de la jornada y selecciona un acceso rápido (“+ Agendar cita”, “+ Nuevo propietario”) o un módulo de trabajo (“Propietarios”, “Mascotas” o “Citas”).<br>3. El sistema abre la pantalla del módulo seleccionado.<br>4. Al finalizar sus actividades en el panel, la recepcionista pulsa la opción “Salir” en el menú superior para cerrar su sesión y regresar al inicio. |
| **Flujos alternos** | 2a. La recepcionista cambia de módulo en cualquier momento empleando la barra de navegación principal (`nav`).<br>2b. La recepcionista pulsa “Salir” directamente desde el panel: el sistema cierra la sesión activa y regresa a la pantalla de inicio de sesión (`index.html`). |
| **Postcondiciones** | La recepcionista accede al módulo operativo seleccionado o regresa a la pantalla de inicio de sesión (`index.html`) al finalizar su jornada. |
| **Reglas y validaciones** | Uso de estructura semántica (`header`, `nav`, `main`, `section`, `article`, `aside`, `footer`) y enlaces de navegación válidos sin enlaces rotos. |
| **Pantallas** | menu-recepcion.html, index.html, propietarios-listado.html, propietarios-nuevo.html, mascotas-listado.html, citas-listado.html, citas-agendar.html |

---

## 3.4. Priorización de casos de uso

El grupo prioriza los casos de uso empleando la técnica **MoSCoW** (*Must, Should, Could, Won’t*), estimando el **Valor de negocio (1–5)** y el **Esfuerzo técnico (1–5)** según la cantidad de pantallas HTML5 y controles de validación requeridos:

| ID | Caso de uso | Valor (1–5) | Esfuerzo (1–5) | Prioridad | Justificación y responsable |
| :--- | :--- | :---: | :---: | :---: | :--- |
| **CU-01** | Iniciar sesión | 5 | 2 | **Must** | Puerta de entrada obligatoria al sistema (`index.html`) que valida correo, contraseña y rol para redirigir a los menús de Recepcionista, Veterinario y Administrador. **Responsable: Integrante 1 (Anthony).** |
| **CU-02** | Gestionar propietarios | 5 | 4 | **Must** | Requisito previo indispensable para registrar mascotas y agendar citas; cubre los 4 flujos CRUD (`propietarios-listado.html`, `propietarios-nuevo.html`, `propietarios-editar.html`, `propietarios-eliminar.html`) validando cédula de 10 dígitos y celular `09XXXXXXXX`. **Responsable: Integrante 1 (Anthony).** |
| **CU-03** | Gestionar mascotas | 5 | 5 | **Must** | La mascota es el paciente central de la clínica; cubre los 4 flujos CRUD (`mascotas-listado.html`, `mascotas-nueva.html`, `mascotas-editar.html`, `mascotas-eliminar.html`) con validación de especie, raza con `datalist`, sexo, fecha de nacimiento y peso (0.1–120 kg). **Responsable: Integrante 2 (Maria).** |
| **CU-04** | Agendar cita | 5 | 4 | **Must** | Es la transacción central del negocio (`citas-agendar.html`, `citas-listado.html`); vincula propietario (`search` con `datalist`), mascota, servicio, veterinario, fecha y hora en bloques de 30 minutos (08:00–17:30) en estado *Programada*. **Responsable: Integrante 3 (Nayia).** |
| **CU-05** | Gestionar citas | 4 | 3 | **Should** | Permite consultar y filtrar citas por estado, reprogramar fecha/hora/veterinario y cancelar citas pasando a estado *Cancelada* con motivo obligatorio (máx. 200 caracteres) y confirmación en `citas-gestionar.html`. **Responsable: Integrante 3 (Nayia).** |
| **CU-06** | Consultar agenda del día | 5 | 2 | **Must** | Vista operativa principal del veterinario (`agenda-veterinario.html`) para consultar sus citas ordenadas por hora según la fecha seleccionada y pasar a atender al paciente o ver su historial. **Responsable: Integrante 3 (Nayia).** |
| **CU-07** | Registrar atención médica | 5 | 3 | **Must** | Permite al veterinario registrar en `atencion-registrar.html` el peso actual (0.1–120 kg), diagnóstico y tratamiento (5–500 caracteres), cambiando el estado de la cita a *Atendida*. **Responsable: Integrante 2 (Maria).** |
| **CU-08** | Consultar historial clínico | 4 | 3 | **Should** | Permite consultar la ficha del paciente, filtrar atenciones previas y ver el detalle clínico completo de cada consulta (`historial-clinico.html`, `historial-detalle.html`). **Responsable: Integrante 2 (Maria).** |
| **CU-09** | Gestionar veterinarios | 3 | 3 | **Should** | Permite al administrador ejecutar los 4 flujos CRUD del personal médico y sus especialidades (`veterinarios-listado.html`, `veterinarios-form.html`, `admin-eliminar.html`) disponible para `CU-04`. **Responsable: Integrante 3 (Nayia).** |
| **CU-10** | Gestionar servicios | 3 | 3 | **Should** | Permite al administrador ejecutar los 4 flujos CRUD del catálogo de servicios (`servicios-listado.html`, `servicios-form.html`, `admin-eliminar.html`) con nombre único y precios validados entre \$1,00 y \$500,00. **Responsable: Integrante 3 (Nayia).** |
| **CU-11** | Consultar panel de recepción | 3 | 1 | **Could** | Permite a la recepcionista visualizar el panel principal con el resumen operativo del día (`menu-recepcion.html`), acceder a los módulos de trabajo y realizar la actividad de salir hacia `index.html`. **Responsable: Integrante 1 (Anthony).** |
