# 📋 Casos de Uso

> **Comentarios:**  
> - Estos casos de uso cubren todas las funcionalidades principales de la plataforma de cursos online y membresías.
> - Se especifican los actores, escenarios principales y alternativos, y restricciones de seguridad.
> - Roles: `ADMIN`, `INSTRUCTOR`, `STUDENT` (usuario autenticado), `Visitante` (no autenticado).
> - Incluye validaciones, seguridad, pagos con Stripe y seguimiento de progreso.

---

## Caso de Uso: Navegación Pública y Exploración de Cursos

**Actor Principal:** Visitante  
**Escenario Principal:**  
1. El visitante accede al sitio y navega por las páginas públicas (inicio, cursos, planes, instructores).
2. Puede explorar el catálogo de cursos con filtros por categoría, precio, nivel de dificultad.
3. Puede ver detalles completos de cada curso, lecciones de vista previa y reseñas.
4. Puede consultar perfiles públicos de instructores y sus cursos.
5. Puede ver planes de membresía disponibles y sus beneficios.

**Restricciones:**  
- Solo muestra cursos publicados y activos.
- Acceso limitado a lecciones de vista previa.
- Optimización SEO y rendimiento para motores de búsqueda.

---

## Caso de Uso: Registro y Autenticación de Usuario

**Actor Principal:** Visitante/Usuario  
**Escenario Principal:**  
1. El visitante completa el formulario de registro con datos personales.
2. El sistema valida la información y crea la cuenta con rol STUDENT por defecto.
3. Se envía email de verificación al usuario.
4. El usuario verifica su email y puede hacer login.
5. Al hacer login, recibe un token JWT para autenticación.

**Escenarios Alternativos:**  
- Si el email ya existe, se informa al usuario.
- Si falla la verificación de email, puede solicitar reenvío.
- Recuperación de contraseña por email con token temporal.

**Restricciones:**  
- Validación de formato de email y fortaleza de contraseña.
- Rate limiting para prevenir ataques de fuerza bruta.
- Tokens JWT con expiración y refresh tokens.

---

## Caso de Uso: Suscripción a Plan de Membresía

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario autenticado selecciona un plan de membresía.
2. Es redirigido al proceso de pago con Stripe.
3. Completa la información de pago y confirma la suscripción.
4. Stripe procesa el pago y envía webhook de confirmación.
5. El sistema activa la membresía y otorga acceso a cursos incluidos.
6. El usuario recibe confirmación por email y acceso inmediato.

**Escenarios Alternativos:**  
- Si el pago falla, se informa al usuario y se puede reintentar.
- Si ya tiene membresía activa, puede actualizar o cambiar plan.
- Cancelación de suscripción con acceso hasta el final del período pagado.

**Restricciones:**  
- Integración segura con Stripe, PCI compliance.
- Manejo de webhooks para sincronización de estados.
- Validación de acceso según estado de membresía.

---

## Caso de Uso: Compra de Curso Individual

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario selecciona un curso específico para comprar.
2. Ve el resumen del curso y precio, procede al checkout.
3. Completa el pago único através de Stripe.
4. El sistema registra la inscripción y otorga acceso inmediato.
5. El usuario puede comenzar a ver el contenido del curso.

**Escenarios Alternativos:**  
- Si el curso ya está incluido en su membresía, se notifica.
- Si el curso es gratuito, se inscribe automáticamente.

**Restricciones:**  
- Validación de que el usuario no esté ya inscrito.
- Registro de transacción para auditoría y soporte.

---

## Caso de Uso: Acceso y Seguimiento de Curso

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario accede a sus cursos desde el dashboard.
2. Selecciona un curso y ve la estructura de módulos y lecciones.
3. Reproduce lecciones en orden, el sistema trackea el progreso automáticamente.
4. Puede descargar recursos adicionales si están disponibles.
5. Completa quizzes y recibe retroalimentación inmediata.
6. Al completar el curso, puede generar su certificado.

**Escenarios Alternativos:**  
- Puede saltar entre lecciones si no son obligatorias.
- Puede revisar lecciones completadas múltiples veces.
- Si falla un quiz obligatorio, debe repetirlo hasta aprobar.

**Restricciones:**  
- Seguimiento preciso de tiempo de visualización.
- Validación de completado de prerrequisitos.
- Límites de descargas según plan de membresía.

---

## Caso de Uso: Realización de Quiz y Evaluación

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario accede a un quiz dentro de una lección.
2. Ve las instrucciones, tiempo límite y número de intentos permitidos.
3. Responde las preguntas dentro del tiempo establecido.
4. Envía el quiz y recibe calificación inmediata.
5. Si aprueba, puede continuar; si no, puede reintentar según las reglas.

**Escenarios Alternativos:**  
- Si se agota el tiempo, el quiz se envía automáticamente.
- Si alcanza el máximo de intentos sin aprobar, se bloquea el progreso.

**Restricciones:**  
- Prevención de trampas (no permitir copiar/pegar, cambiar pestañas).
- Almacenamiento seguro de respuestas y resultados.

---

## Caso de Uso: Generación y Descarga de Certificado

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario completa todos los requisitos del curso (lecciones y quizzes).
2. El sistema valida el completado y genera automáticamente el certificado.
3. Se crea un PDF personalizado con datos del usuario y curso.
4. El certificado recibe un número único para verificación.
5. El usuario puede descargar y compartir el certificado.

**Restricciones:**  
- Solo se genera si se cumplen todos los requisitos.
- Certificado con marca de agua y datos de verificación.
- Registro en blockchain o sistema de verificación pública.

---

## Caso de Uso: Escritura y Moderación de Reseñas

**Actor Principal:** STUDENT  
**Escenario Principal:**  
1. El usuario que ha completado al menos 50% del curso puede escribir una reseña.
2. Califica el curso (1-5 estrellas) y escribe comentarios.
3. La reseña queda pendiente de moderación.
4. Un ADMIN revisa y aprueba/rechaza la reseña.
5. Las reseñas aprobadas se muestran públicamente.

**Restricciones:**  
- Solo usuarios inscritos pueden reseñar.
- Una reseña por usuario por curso.
- Moderación obligatoria para evitar spam y contenido inapropiado.

---

## Caso de Uso: Creación y Gestión de Curso (Instructor)

**Actor Principal:** INSTRUCTOR o ADMIN  
**Escenario Principal:**  
1. El instructor accede al panel de creación de cursos.
2. Completa información básica del curso (título, descripción, precio, categoría).
3. Crea módulos y estructura el contenido.
4. Añade lecciones con videos, texto, recursos y quizzes.
5. Configura vista previa y publica el curso.
6. Puede monitorear estadísticas y progreso de estudiantes.

**Escenarios Alternativos:**  
- Puede guardar como borrador y continuar editando.
- Puede despublicar curso temporalmente para actualizaciones.

**Restricciones:**  
- Validación de contenido multimedia y tamaños de archivo.
- Solo instructores pueden editar sus propios cursos (ADMIN puede editar todos).
- Logs de cambios para auditoría.

---

## Caso de Uso: Subida y Gestión de Contenido Multimedia

**Actor Principal:** INSTRUCTOR o ADMIN  
**Escenario Principal:**  
1. El instructor accede al gestor de archivos multimedia.
2. Selecciona archivos (videos, PDFs, imágenes) para subir.
3. El sistema valida tipo, tamaño y ejecuta escaneo antivirus.
4. Los archivos se almacenan en servicio cloud (S3) o local.
5. Puede organizar, renombrar y eliminar archivos.
6. Puede asociar archivos a lecciones específicas.

**Restricciones:**  
- Límites de tamaño y tipo de archivo por plan.
- Compresión automática de videos para optimizar streaming.
- Control de acceso basado en inscripciones.

---

## Caso de Uso: Administración de Usuarios y Roles

**Actor Principal:** ADMIN  
**Escenario Principal:**  
1. El administrador accede al panel de gestión de usuarios.
2. Puede ver lista completa con filtros y búsqueda.
3. Puede crear nuevos usuarios asignando roles específicos.
4. Puede editar información, cambiar roles y estados de cuenta.
5. Puede suspender o eliminar usuarios según políticas.
6. Puede ver historial de actividad y logs de acceso.

**Restricciones:**  
- Solo ADMIN puede gestionar usuarios y asignar roles.
- Auditoría completa de cambios realizados.
- No puede eliminar su propia cuenta de ADMIN.

---

## Caso de Uso: Gestión de Planes de Membresía

**Actor Principal:** ADMIN  
**Escenario Principal:**  
1. El administrador accede a la gestión de planes.
2. Puede crear nuevos planes definiendo precio, duración y beneficios.
3. Configura qué cursos están incluidos en cada plan.
4. Establece límites (descargas, cursos simultáneos, etc.).
5. Puede activar/desactivar planes y modificar precios.
6. Ve reportes de suscripciones y ingresos por plan.

**Restricciones:**  
- Cambios en planes activos requieren migración cuidadosa.
- Integración con Stripe para productos y precios.

---

## Caso de Uso: Procesamiento de Pagos y Webhooks

**Actor Principal:** Sistema (Stripe)  
**Escenario Principal:**  
1. Stripe procesa un pago y envía webhook al sistema.
2. El sistema valida la autenticidad del webhook.
3. Actualiza el estado de la transacción en la base de datos.
4. Activa membresía o inscripción según el tipo de pago.
5. Envía notificación de confirmación al usuario.
6. Registra evento para auditoría y reportes.

**Escenarios Alternativos:**  
- Si el pago falla, notifica al usuario y permite reintentar.
- Para suscripciones, maneja renovaciones automáticas.
- Para cancelaciones, mantiene acceso hasta fin del período.

**Restricciones:**  
- Validación criptográfica de webhooks de Stripe.
- Idempotencia para evitar procesamiento duplicado.
- Manejo de errores y reintentos automáticos.

---

## Caso de Uso: Generación de Reportes y Analytics

**Actor Principal:** ADMIN o INSTRUCTOR  
**Escenario Principal:**  
1. El usuario accede al dashboard de analytics.
2. Selecciona período de tiempo y métricas de interés.
3. Ve gráficos de inscripciones, completados, ingresos.
4. Puede filtrar por curso, categoría o instructor.
5. Exporta reportes en formato PDF o Excel.
6. Configura reportes automáticos por email.

**Restricciones:**  
- INSTRUCTOR solo ve datos de sus propios cursos.
- ADMIN tiene acceso completo a todas las métricas.
- Datos anonimizados para cumplir con GDPR.

---

## Buenas Prácticas y Seguridad (aplica a todos los casos)

- Validación y sanitización de entrada en todos los formularios.
- Autenticación JWT con refresh tokens y expiración.
- Autorización granular basada en roles y propiedad de recursos.
- Rate limiting para prevenir abuso de APIs.
- Logs detallados de acciones críticas y transacciones.
- Cumplimiento de PCI DSS para manejo de pagos.
- Protección contra XSS, CSRF y inyección SQL.
- Backup automático y plan de recuperación ante desastres.

---