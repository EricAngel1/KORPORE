# Guía para llenar historias de usuario de Korpore

Esta guía explica cómo utilizar la plantilla de historias de usuario, qué escribir en cada apartado y cómo redactar criterios de aceptación claros.

Los ejemplos son ilustrativos: no representan requisitos confirmados de Korpore. Adapten los roles, funcionalidades y reglas a lo acordado por el equipo.

## 1. ¿Qué es una historia de usuario?

Es una descripción breve de una necesidad desde el punto de vista de quien utilizará el sistema. Explica quién necesita algo, qué necesita y qué beneficio obtiene.

Una historia debe centrarse en una necesidad concreta. Por ejemplo, «Iniciar sesión» y «Recuperar contraseña» pueden ser historias distintas.

## 2. Plantilla base

Copia esta plantilla y sustituye los textos entre corchetes. Los corchetes son indicaciones; no deben quedarse en la historia terminada.

````markdown
---
name: Historia de usuario
about: Esta plantilla sirve para crear historias de usuario
title: ''
labels: ''
assignees: ''

---

**Como** [rol]  
**Necesito** [funcionalidad]  
**Para** [beneficio]  

### Detalles y supuestos
* [documenta lo que sabes]

### Criterios de aceptación

```gherkin
# language: es
Dado [un contexto]
Cuando [se realiza una acción]
Entonces [se observa el resultado de la acción]
```
````

## 3. Configuración inicial: el bloque entre `---`

Este bloque configura la plantilla. Se define al preparar el archivo de plantilla; normalmente no se vuelve a escribir dentro de cada issue creado con ella.

| Campo | Qué significa | Qué pueden poner |
|---|---|---|
| `name` | Nombre que identifica la plantilla. | `Historia de usuario` |
| `about` | Explicación breve de para qué se utiliza. | `Esta plantilla sirve para crear historias de usuario` |
| `title` | Texto predeterminado del título de los nuevos issues. | `''` para dejarlo vacío o `'[HU] '` como prefijo. |
| `labels` | Etiquetas que se aplicarán automáticamente. | `''` si las elegirán al crear cada issue. Si especifican alguna, debe existir en el repositorio. |
| `assignees` | Usuarios que se asignarán automáticamente como responsables. | `''` si el responsable se decidirá para cada historia. Si lo llenan, utilicen un usuario de GitHub que pueda recibir la asignación. |

**Importante:** conserva las claves `name`, `about`, `title`, `labels` y `assignees` en inglés. Puedes traducir sus valores, pero las claves forman parte de la configuración.

Para Korpore pueden mantener exactamente los valores de la plantilla base y elegir etiquetas y responsables en cada issue.

## 4. Cómo escribir el título del issue

Escribe una acción concreta y fácil de identificar. El título se completa en el campo de título del issue.

| Título poco claro | Título más claro |
|---|---|
| Usuarios | Registrar una cuenta de usuario |
| Login | Iniciar sesión con correo y contraseña |
| Cambios | Actualizar el nombre del perfil |

Si usan el prefijo `[HU]`, un título completo sería: **[HU] Iniciar sesión con correo y contraseña**.

## 5. Cómo llenar la historia

### «Como»: quién tiene la necesidad

Escribe el rol de la persona que utilizará la funcionalidad, no el nombre del compañero que la programará.

Ejemplos: visitante, usuario registrado o administrador, siempre que esos roles existan en Korpore.

> **Como** usuario registrado

### «Necesito»: qué quiere hacer

Describe una acción concreta del usuario. Evita juntar funcionalidades que podrían entregarse por separado.

> **Necesito** iniciar sesión con mi correo y contraseña

### «Para»: qué beneficio obtiene

Explica para qué le sirve esa acción. No repitas la funcionalidad con otras palabras.

> **Para** acceder a mi cuenta y a las funciones que tengo autorizadas

Historia completa:

> **Como** usuario registrado  
> **Necesito** iniciar sesión con mi correo y contraseña  
> **Para** acceder a mi cuenta y a las funciones que tengo autorizadas

## 6. Cómo llenar «Detalles y supuestos»

Agrega la información necesaria para entender la historia y sus límites: datos solicitados, permisos, validaciones y decisiones pendientes.

Aunque la plantilla los agrupa, identifica qué está confirmado y qué falta validar:

```markdown
### Detalles y supuestos
* Detalle confirmado: el inicio de sesión solicita correo y contraseña.
* Detalle confirmado: ambos campos son obligatorios.
* Detalle confirmado: las credenciales incorrectas muestran un mensaje general.
* Fuera de alcance: la recuperación de contraseña se atenderá en otra historia.
* Supuesto por validar: después de iniciar sesión se mostrará una pantalla de inicio común para todos los roles.
```

No presentes un supuesto como una regla aprobada. Si no hay dudas pendientes, puedes escribir «Sin supuestos pendientes».

## 7. Cómo escribir los criterios de aceptación

Son las condiciones que deben cumplirse para aceptar la funcionalidad. Deben permitir que otra persona compruebe el resultado.

| Parte | Qué debes escribir | Pregunta que responde |
|---|---|---|
| `Dado` | Situación inicial y condiciones necesarias. | ¿Qué ocurre antes de la acción? |
| `Cuando` | Acción que activa el comportamiento. | ¿Qué hace el usuario? |
| `Entonces` | Resultado esperado, concreto y verificable. | ¿Qué debe pasar? |

Ejemplo:

```gherkin
# language: es
Dado que tengo una cuenta registrada y no he iniciado sesión
Cuando envío el formulario con un correo y una contraseña válidos
Entonces accedo a mi cuenta y veo la pantalla de inicio
```

La línea `# language: es` indica que el ejemplo utiliza palabras clave en español. `Y` permite agregar condiciones o resultados relacionados.

Incluye un escenario para el flujo principal y los casos de error que correspondan. Usa varios bloques si eso facilita la lectura.

| Evita escribir | Escribe algo comprobable |
|---|---|
| El sistema funciona correctamente. | Al guardar un nombre válido, el perfil muestra el nuevo nombre. |
| Se valida el formulario. | Si falta el correo, se muestra una indicación y no se envía el formulario. |
| Se muestra un error. | Se muestra «Correo o contraseña incorrectos» y no se inicia sesión. |

## 8. Ejemplo completo: iniciar sesión

**Título del issue:** `[HU] Iniciar sesión con correo y contraseña`

El siguiente bloque es el cuerpo de un issue ya llenado. No incluye la configuración inicial de la plantilla.

````markdown
**Como** usuario registrado  
**Necesito** iniciar sesión con mi correo y contraseña  
**Para** acceder a mi cuenta y a las funciones que tengo autorizadas  

### Detalles y supuestos
* El formulario solicita correo y contraseña.
* Ambos campos son obligatorios.
* La contraseña no debe mostrarse en texto visible mientras se escribe.
* Si las credenciales son incorrectas, se muestra un mensaje general.
* La recuperación de contraseña se atenderá en otra historia.
* Supuesto por validar: todos los roles acceden inicialmente a la misma pantalla de inicio.

### Criterios de aceptación

**Escenario 1: Inicio de sesión exitoso**
```gherkin
# language: es
Dado que tengo una cuenta registrada y no he iniciado sesión
Cuando envío el formulario con mi correo y contraseña correctos
Entonces se inicia mi sesión
Y veo la pantalla de inicio acordada por el equipo
```

**Escenario 2: Credenciales incorrectas**
```gherkin
# language: es
Dado que no he iniciado sesión
Cuando envío un correo y una contraseña que no corresponden a una cuenta válida
Entonces veo el mensaje "Correo o contraseña incorrectos"
Y no se inicia una sesión
```

**Escenario 3: Campo obligatorio vacío**
```gherkin
# language: es
Dado que estoy en el formulario de inicio de sesión
Cuando intento enviarlo con el correo o la contraseña vacíos
Entonces se indican los campos obligatorios que faltan
Y no se inicia una sesión
```
````

## 9. Ejemplo completo: actualizar el nombre del perfil

**Título del issue:** `[HU] Actualizar el nombre del perfil`

La regla de longitud de este ejemplo es una decisión ilustrativa, no un requisito confirmado de Korpore.

````markdown
**Como** usuario registrado  
**Necesito** modificar el nombre que aparece en mi perfil  
**Para** mantener actualizada mi información personal  

### Detalles y supuestos
* El usuario debe tener una sesión iniciada.
* Cada usuario puede modificar únicamente su propio perfil.
* El nombre debe contener entre 2 y 80 caracteres después de quitar espacios al inicio y al final.
* No se modifican el correo ni la contraseña desde esta funcionalidad.
* Sin supuestos pendientes para este ejemplo.

### Criterios de aceptación

**Escenario 1: Guardar un nombre válido**
```gherkin
# language: es
Dado que tengo una sesión iniciada y estoy editando mi perfil
Cuando cambio mi nombre por "Juan Pablo" y guardo los cambios
Entonces veo una confirmación de actualización
Y mi perfil muestra "Juan Pablo" al volver a abrirlo
```

**Escenario 2: Nombre vacío**
```gherkin
# language: es
Dado que estoy editando mi perfil
Cuando intento guardar el nombre vacío o formado solo por espacios
Entonces veo una indicación de que el nombre es obligatorio
Y se conserva el nombre anterior
```

**Escenario 3: Nombre fuera del límite permitido**
```gherkin
# language: es
Dado que estoy editando mi perfil
Cuando intento guardar un nombre de 1 carácter o de más de 80 caracteres
Entonces veo una indicación de que el nombre debe tener entre 2 y 80 caracteres
Y se conserva el nombre anterior
```

**Escenario 4: Intentar modificar un perfil ajeno**
```gherkin
# language: es
Dado que tengo una sesión iniciada con mi propia cuenta
Cuando intento enviar una modificación para el perfil de otro usuario
Entonces el sistema rechaza la modificación
Y los datos del otro usuario permanecen sin cambios
```
````

## 10. Revisión antes de publicar el issue

- [ ] El título describe una funcionalidad concreta.
- [ ] El rol corresponde a alguien que utilizará el sistema.
- [ ] La necesidad y el beneficio se entienden sin explicaciones adicionales.
- [ ] Los detalles y las reglas coinciden con lo acordado por el equipo.
- [ ] Los supuestos están identificados como pendientes de validar.
- [ ] Los criterios incluyen el flujo principal y los errores relevantes.
- [ ] Cada resultado puede comprobarse mediante una prueba.
- [ ] Se sustituyeron todos los textos entre corchetes.
- [ ] Los permisos y límites descritos tienen criterios para comprobarlos cuando corresponde.

## 11. Cómo usarla en el equipo

1. Acuerden la necesidad, las reglas y el alcance antes de dar la historia por lista para desarrollar.
2. Creen un issue por historia y completen el título y el cuerpo.
3. Seleccionen al responsable y las etiquetas que correspondan.
4. Gestionen prioridad, estimación, estado y sprint en los campos del tablero, si los tienen configurados.
5. Antes de cerrar la historia, comprueben todos los criterios de aceptación y registren la evidencia necesaria.

Una historia describe el resultado que necesita el usuario. Las tareas técnicas para conseguirlo, como crear un endpoint o modificar una tabla, pueden registrarse por separado o como una lista de trabajo dentro del issue.
