# Reflexión sobre el proyecto MiniVault

## 🔹 Ciclo de vida del dato (5b)

### 1. ¿Cómo se gestionan los datos desde su generación hasta su eliminación?

En mi proyecto los datos se generan cuando el usuario crea una nueva credencial (servicio, usuario, contraseña y notas).

Estos datos no se guardan en texto plano. Antes de almacenarse, se cifran automáticamente usando la contraseña maestra del usuario. Después se guardan en un archivo local llamado `vault.json`.

Cuando el usuario abre la aplicación e introduce su contraseña, los datos se descifran temporalmente en memoria para poder mostrarlos en la interfaz.

Si se edita una credencial, el archivo completo se vuelve a cifrar con los cambios aplicados.  
Si se elimina una credencial, desaparece del archivo al guardarse de nuevo.

Además, cuando se copia una contraseña, el portapapeles se limpia automáticamente después de unos segundos para evitar riesgos.

---

### 2. ¿Qué estrategia sigues para garantizar la consistencia e integridad de los datos?

Para garantizar la integridad:

- Cada credencial tiene un identificador único.
- El archivo siempre se guarda completo y cifrado.
- Si el archivo se modifica manualmente, el sistema detecta un error al intentar descifrarlo.
- Solo se puede acceder con la contraseña maestra correcta.
- No se permiten entradas incompletas.

---

### 3. Si no trabajas con datos, ¿cómo podrías incluir una funcionalidad que los gestione de forma eficiente?

En mi caso sí trabajo con datos, pero podría mejorar la gestión añadiendo:

- Copias de seguridad automáticas.
- Exportación cifrada.
- Historial de cambios.
- Control de versiones del archivo.

---

## ☁️ Almacenamiento en la nube (5f)

### 1. Si tu software utiliza almacenamiento en la nube, ¿cómo garantizas la seguridad y disponibilidad?

Actualmente MiniVault no utiliza almacenamiento en la nube. Todo se guarda en local en el ordenador del usuario.

Esto reduce riesgos, ya que los datos no salen del dispositivo.

Si se implementara nube en el futuro, se garantizaría la seguridad mediante:

- Cifrado extremo a extremo (cifrar antes de subir).
- No almacenar la contraseña maestra en servidores.
- Autenticación segura y control de accesos.

---

### 2. ¿Qué alternativas consideraste y por qué elegiste la actual?

Las alternativas podrían haber sido:

- Base de datos local.
- Servidor online propio.
- Sincronización en la nube.

Elegí archivo JSON cifrado en local porque:

- Es más sencillo.
- No necesita servidor.
- No tiene costes.
- Es más privado.
- Es adecuado para un usuario individual.

---

### 3. Si no usas la nube, ¿cómo podrías integrarla en futuras versiones?

Se podría integrar mediante:

- Sincronización del archivo cifrado con Google Drive o Dropbox.
- Copias cifradas automáticas en la nube.
- Un backend propio (API) para sincronizar.

Siempre manteniendo el cifrado antes de subir los datos.

---

## 🔐 Seguridad y regulación (5i)

### 1. ¿Qué medidas de seguridad implementaste para proteger los datos o procesos?

- Cifrado fuerte de las credenciales.
- La clave depende de la contraseña maestra.
- Uso de un salt aleatorio para evitar ataques simples.
- Limpieza automática del portapapeles tras copiar contraseñas.
- Auto-bloqueo por inactividad (opcional).
- Opción de ocultar usuarios en la tabla.

Las contraseñas nunca se guardan en texto plano.

---

### 2. ¿Qué normativas (ej. GDPR) podrían afectar el uso del software y cómo las has tenido en cuenta?

Podría afectar el GDPR si se usara en empresa, porque se guardan datos personales (usuarios/correos y contraseñas).

En mi caso, como es una app local y no envía datos a internet, el impacto es menor. Aun así, el hecho de cifrar los datos y no compartirlos ayuda a proteger la privacidad. Si se publicara como producto, habría que añadir una política de privacidad y advertencias claras.

---

### 3. Si no implementaste medidas de seguridad, ¿qué riesgos potenciales identificas y cómo los abordarías?

En mi proyecto sí hay medidas, pero los riesgos principales serían:

- Olvidar la contraseña maestra (no se puede recuperar).
- Malware en el equipo que lea lo que se copia al portapapeles.
- Robo del ordenador.

En el futuro se podría mejorar con:

- Autenticación biométrica o doble factor.
- Copias de seguridad cifradas.
- Opciones para limitar aún más el copiado o avisos de seguridad.

---

## 🏭 Implicación de las THD en negocio y planta (2e)

### 1. ¿Qué impacto tendría tu software en un entorno de negocio o en una planta industrial?

En un negocio ayudaría a centralizar credenciales y evitar compartirlas por WhatsApp, papel o correo. Esto reduce riesgos y mejora la organización.

En una planta industrial también puede ser útil para guardar accesos a sistemas técnicos (servidores, paneles, equipos, software interno), ya que ahí un fallo de seguridad puede afectar a procesos críticos.

---

### 2. ¿Cómo crees que tu solución podría mejorar procesos operativos o la toma de decisiones?

Mejora procesos porque:

- Ahorra tiempo buscando contraseñas.
- Reduce errores humanos (contraseñas mal apuntadas o repetidas).
- Aumenta la seguridad y el control.
- Facilita el trabajo cuando varias cuentas se usan diariamente.

---

### 3. Si tu proyecto no aplica directamente a negocio o planta, ¿qué otros entornos podrían beneficiarse?

Puede beneficiar a:

- Autónomos (gestión de muchas cuentas).
- Equipos IT pequeños.
- Estudiantes y desarrolladores.
- Cualquier persona que quiera ordenar y proteger sus accesos.

---

## 🔄 Mejoras en IT y OT (2f)

### 1. ¿Cómo puede tu software facilitar la integración entre entornos IT y OT?

Puede ayudar porque centraliza y protege credenciales de sistemas IT (servidores, herramientas, redes) y OT (sistemas industriales o técnicos). Tener accesos organizados reduce fallos y accesos indebidos.

---

### 2. ¿Qué procesos específicos podrían beneficiarse en términos de automatización o eficiencia?

- Control básico de contraseñas en equipos compartidos.
- Menos tiempo perdido recuperando accesos o reseteando cuentas.

---

### 3. Si no aplica a IT u OT, ¿cómo podrías adaptarlo para mejorar procesos tecnológicos concretos?

Se podría adaptar para:

- Sincronización segura entre varios dispositivos.

---

## 🚀 Tecnologías Habilitadoras Digitales (2g)

### 1. ¿Qué tecnologías habilitadoras digitales (THD) has utilizado o podrías integrar?

He utilizado principalmente:

- Ciberseguridad (cifrado de datos).
- Automatización (auto-bloqueo y borrado del portapapeles).
- Interfaz digital de escritorio.
- Desarrollo de software para resolver una necesidad real.

---

### 2. ¿Cómo mejoran estas tecnologías la funcionalidad o el alcance del software?

- El cifrado permite guardar datos sensibles con más seguridad.
- La automatización reduce errores humanos (por ejemplo, olvidar el portapapeles con la contraseña).
- La interfaz mejora la facilidad de uso, haciendo que el programa sea accesible para cualquiera.

---

### 3. Si no has utilizado THD, ¿cómo podrías implementarlas en el futuro para enriquecer la solución?

En futuras versiones podría añadir:

- Sincronización cifrada en la nube.
- Evaluación inteligente de contraseñas (para recomendar mejoras).
- Autenticación biométrica.
- Integración con gestores de identidad o sistemas empresariales.
