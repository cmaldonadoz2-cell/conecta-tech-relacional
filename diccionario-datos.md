# Diccionario de Datos

## 1. Persona

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_persona | INTEGER | PK, IDENTITY | Identificador único de la persona |
| nombre | VARCHAR(120) | NOT NULL | Nombre completo |
| correo | VARCHAR(150) | NOT NULL, UNIQUE | Correo electrónico |
| pais | VARCHAR(80) | NOT NULL | País de procedencia |

## 2. Edición

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_edicion | INTEGER | PK, IDENTITY | Identificador de la edición |
| nombre | VARCHAR(150) | NOT NULL | Nombre del congreso |
| anio | INTEGER | NOT NULL | Año de la edición |
| fecha_inicio | DATE | NOT NULL | Fecha de inicio |
| fecha_fin | DATE | NOT NULL | Fecha de finalización |
| estado_preparacion | VARCHAR(20) | NOT NULL | Estado de preparación |
| modalidad | VARCHAR(15) | NOT NULL | Presencial, virtual o híbrida |

## 3. Sede

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_sede | INTEGER | PK, IDENTITY | Identificador de la sede |
| nombre | VARCHAR(120) | NOT NULL | Nombre de la sede |
| direccion | VARCHAR(200) | NOT NULL | Dirección |
| ciudad | VARCHAR(80) | NOT NULL | Ciudad donde se encuentra |

## 4. Sala

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_sala | INTEGER | PK, IDENTITY | Identificador de la sala |
| id_sede | INTEGER | FK, NOT NULL | Sede a la que pertenece |
| nombre | VARCHAR(100) | NOT NULL | Nombre de la sala |
| capacidad | INTEGER | NOT NULL, CHECK | Capacidad máxima |

## 5. Sesión

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_sesion | INTEGER | PK, IDENTITY | Identificador de la sesión |
| id_edicion | INTEGER | FK, NOT NULL | Edición a la que pertenece |
| id_sala | INTEGER | FK | Sala utilizada |
| titulo | VARCHAR(200) | NOT NULL | Título de la sesión |
| resumen | TEXT | NOT NULL | Resumen de la sesión |
| fecha | DATE | NOT NULL | Fecha de realización |
| hora_inicial | TIME | NOT NULL | Hora de inicio |
| hora_final | TIME | NOT NULL | Hora de finalización |
| tipo | VARCHAR(10) | NOT NULL | Charla o taller |

## 6. Transmisión

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_transmision | INTEGER | PK, IDENTITY | Identificador de transmisión |
| id_sesion | INTEGER | FK, UNIQUE | Sesión transmitida |
| plataforma | VARCHAR(80) | NOT NULL | Plataforma utilizada |
| enlace | TEXT | NOT NULL | Enlace de transmisión |
| codigo_acceso | VARCHAR(100) | | Código de acceso |

## 7. Acreditación

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_acreditacion | INTEGER | PK, IDENTITY | Identificador |
| nombre | VARCHAR(80) | NOT NULL, UNIQUE | Nombre del tipo de acreditación |
| descripcion | TEXT | | Descripción |

## 8. Inscripción a Edición

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_inscripcion_edicion | INTEGER | PK, IDENTITY | Identificador |
| id_persona | INTEGER | FK, NOT NULL | Persona inscrita |
| id_edicion | INTEGER | FK, NOT NULL | Edición |
| rol_asistente | BOOLEAN | NOT NULL, DEFAULT | Indica si es asistente |
| rol_ponente | BOOLEAN | NOT NULL, DEFAULT | Indica si es ponente |
| id_acreditacion | INTEGER | FK | Tipo de acreditación |

## 9. Perfil de Ponente

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_persona | INTEGER | PK, FK | Persona que es ponente |
| biografia | TEXT | NOT NULL | Biografía profesional |

## 10. Inscripción a Sesión

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_inscripcion_sesion | INTEGER | PK, IDENTITY | Identificador |
| id_inscripcion_edicion | INTEGER | FK, NOT NULL | Inscripción de la persona |
| id_sesion | INTEGER | FK, NOT NULL | Sesión |
| fecha_inscripcion | DATE | NOT NULL | Fecha de inscripción |
| estado | VARCHAR(20) | NOT NULL | Estado de la inscripción |
| asistencia | BOOLEAN | | Indica si asistió |

## 11. Asignación de Ponente

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_sesion | INTEGER | PK, FK | Sesión |
| id_persona | INTEGER | PK, FK | Ponente |
| rol_ponente | VARCHAR(80) | NOT NULL | Rol del ponente |
| orden_programa | INTEGER | NOT NULL | Orden de aparición |

## 12. Prerrequisito

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_sesion | INTEGER | PK, FK | Sesión que tiene el requisito |
| id_sesion_previa | INTEGER | PK, FK | Sesión que debe realizarse previamente |

## 13. Empresa

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_empresa | INTEGER | PK, IDENTITY | Identificador |
| nombre | VARCHAR(150) | NOT NULL, UNIQUE | Nombre de la empresa |
| correo | VARCHAR(150) | NOT NULL | Correo de contacto |
| telefono | VARCHAR(30) | | Teléfono |

## 14. Acuerdo de Patrocinio

| Campo | Tipo | Restricciones | Descripción |
|---|---|---|---|
| id_empresa | INTEGER | PK, FK | Empresa patrocinadora |
| id_edicion | INTEGER | PK, FK | Edición patrocinada |
| categoria | VARCHAR(50) | NOT NULL | Categoría del patrocinio |
| monto | NUMERIC(12,2) | NOT NULL, CHECK | Monto aportado |
| fecha_confirmacion | DATE | NOT NULL | Fecha de confirmación |

## Claves candidatas importantes

- Persona: `correo`
- Acreditación: `nombre`
- Empresa: `nombre`
- Inscripción a edición: `(id_persona, id_edicion)`
- Inscripción a sesión: `(id_inscripcion_edicion, id_sesion)`
- Asignación de ponente: `(id_sesion, id_persona)`
- Prerrequisito: `(id_sesion, id_sesion_previa)`
- Acuerdo de patrocinio: `(id_empresa, id_edicion)`
- Transmisión: `id_sesion`

## Dominios principales

### Modalidad de edición
- presencial
- virtual
- híbrida

### Estado de preparación
- planificada
- en_preparacion
- lista
- finalizada
- cancelada

### Tipo de sesión
- charla
- taller

### Estado de inscripción
- inscrita
- cancelada
- confirmada
- lista_espera

### Asistencia
- TRUE
- FALSE
- NULL mientras todavía no se registra