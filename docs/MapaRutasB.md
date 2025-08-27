# 🛣️ Mapa de rutas Backend (API RESTful)

> **Comentarios:**  
> - Este mapa describe las rutas principales de la API para la plataforma de cursos online y membresías.  
> - Basado en el modelo relacional y entidades del ERD proporcionado.
> - Roles soportados: `ADMIN`, `INSTRUCTOR`, `STUDENT` (usuarios autenticados), y `guest` (no autenticado).
> - Autenticación JWT, validación de permisos, integración con Stripe y seguridad en cada endpoint.

---

## Rutas públicas (sin autenticación)

| Método | Ruta                             | Descripción                                      | Roles       |
|--------|----------------------------------|--------------------------------------------------|-------------|
| GET    | /api/courses                     | Listar cursos públicos (publicados)             | Todos       |
| GET    | /api/courses/:slug               | Ver detalle de curso                             | Todos       |
| GET    | /api/courses/:slug/preview       | Ver lecciones de vista previa                    | Todos       |
| GET    | /api/categories                  | Listar categorías activas                        | Todos       |
| GET    | /api/categories/:slug            | Listar cursos por categoría                      | Todos       |
| GET    | /api/membership-plans            | Listar planes de membresía activos               | Todos       |
| GET    | /api/instructors                 | Listar instructores públicos                     | Todos       |
| GET    | /api/instructors/:id             | Perfil público de instructor                     | Todos       |
| GET    | /api/courses/:slug/reviews       | Listar reseñas aprobadas del curso               | Todos       |
| GET    | /api/certificates/verify/:number | Verificar autenticidad de certificado            | Todos       |
| GET    | /api/site-settings/public        | Configuración pública del sitio                  | Todos       |

---

## Rutas de autenticación y usuario

| Método | Ruta                             | Descripción                                      | Roles             |
|--------|----------------------------------|--------------------------------------------------|-------------------|
| POST   | /api/auth/register               | Registro de nuevo usuario                        | Todos             |
| POST   | /api/auth/login                  | Login y obtención de token JWT                   | Todos             |
| POST   | /api/auth/logout                 | Logout (invalidar sesión/token)                  | Usuarios          |
| POST   | /api/auth/refresh                | Refrescar token JWT                              | Usuarios          |
| GET    | /api/auth/me                     | Obtener datos del usuario autenticado           | Usuarios          |
| PUT    | /api/auth/profile                | Editar perfil del usuario                        | Usuarios          |
| PUT    | /api/auth/change-password        | Cambiar contraseña                               | Usuarios          |
| POST   | /api/auth/password-reset         | Solicitar recuperación de contraseña             | Todos             |
| POST   | /api/auth/password-reset/confirm | Confirmar recuperación de contraseña             | Todos             |
| POST   | /api/auth/verify-email           | Verificar email con token                        | Todos             |
| GET    | /api/users/dashboard             | Dashboard personalizado del usuario              | Usuarios          |

---

## Rutas de membresías y pagos

| Método | Ruta                             | Descripción                                      | Roles             |
|--------|----------------------------------|--------------------------------------------------|-------------------|
| GET    | /api/memberships/my              | Ver membresía actual del usuario                 | Usuarios          |
| POST   | /api/memberships/subscribe       | Suscribirse a un plan de membresía               | Usuarios          |
| PUT    | /api/memberships/cancel          | Cancelar suscripción activa                      | Usuarios          |
| PUT    | /api/memberships/reactivate      | Reactivar suscripción cancelada                  | Usuarios          |
| GET    | /api/payments/history            | Historial de pagos del usuario                   | Usuarios          |
| POST   | /api/payments/process            | Procesar pago de curso individual                | Usuarios          |
| POST   | /api/payments/stripe/webhook     | Webhook de Stripe para eventos de pago           | Sistema           |

---

## Rutas de cursos y contenido (estudiantes)

| Método | Ruta                             | Descripción                                      | Roles             |
|--------|----------------------------------|--------------------------------------------------|-------------------|
| GET    | /api/enrollments/my              | Mis cursos inscritos                             | Usuarios          |
| POST   | /api/courses/:id/enroll          | Inscribirse a un curso                           | Usuarios          |
| GET    | /api/courses/:id/content         | Acceder al contenido del curso                   | Usuarios          |
| GET    | /api/courses/:id/modules         | Listar módulos del curso                         | Usuarios          |
| GET    | /api/modules/:id/lessons         | Listar lecciones del módulo                      | Usuarios          |
| GET    | /api/lessons/:id                 | Ver contenido de la lección                      | Usuarios          |
| PUT    | /api/lessons/:id/progress        | Actualizar progreso de lección                   | Usuarios          |
| POST   | /api/lessons/:id/complete        | Marcar lección como completada                   | Usuarios          |
| GET    | /api/lessons/:id/resources       | Descargar recursos de la lección                 | Usuarios          |
| GET    | /api/quizzes/:id                 | Ver quiz de la lección                           | Usuarios          |
| POST   | /api/quizzes/:id/attempt         | Intentar quiz                                    | Usuarios          |
| GET    | /api/quizzes/:id/results         | Ver resultados del quiz                          | Usuarios          |
| POST   | /api/courses/:id/review          | Escribir reseña del curso                        | Usuarios          |
| GET    | /api/certificates/my             | Mis certificados obtenidos                       | Usuarios          |
| GET    | /api/certificates/:id/download   | Descargar certificado                            | Usuarios          |

---

## Rutas administrativas de cursos (INSTRUCTOR, ADMIN)

| Método | Ruta                             | Descripción                                      | Roles               |
|--------|----------------------------------|--------------------------------------------------|---------------------|
| GET    | /api/instructor/courses          | Listar cursos del instructor                     | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/courses          | Crear nuevo curso                                | INSTRUCTOR, ADMIN   |
| GET    | /api/instructor/courses/:id      | Ver detalle del curso                            | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/courses/:id      | Editar curso                                     | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/courses/:id      | Eliminar curso                                   | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/courses/:id/publish | Publicar/despublicar curso                    | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/courses/:id/modules | Crear módulo en curso                         | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/modules/:id      | Editar módulo                                    | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/modules/:id      | Eliminar módulo                                  | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/modules/:id/lessons | Crear lección en módulo                       | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/lessons/:id      | Editar lección                                   | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/lessons/:id      | Eliminar lección                                 | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/lessons/:id/resources | Subir recurso a lección                      | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/resources/:id    | Eliminar recurso                                 | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/lessons/:id/quiz | Crear quiz para lección                          | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/quizzes/:id      | Editar quiz                                      | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/quizzes/:id      | Eliminar quiz                                    | INSTRUCTOR, ADMIN   |
| POST   | /api/instructor/quizzes/:id/questions | Crear pregunta de quiz                      | INSTRUCTOR, ADMIN   |
| PUT    | /api/instructor/questions/:id    | Editar pregunta                                  | INSTRUCTOR, ADMIN   |
| DELETE | /api/instructor/questions/:id    | Eliminar pregunta                                | INSTRUCTOR, ADMIN   |
| GET    | /api/instructor/students         | Listar estudiantes de mis cursos                 | INSTRUCTOR, ADMIN   |
| GET    | /api/instructor/analytics        | Estadísticas de mis cursos                       | INSTRUCTOR, ADMIN   |

---

## Rutas administrativas del sistema (solo ADMIN)

| Método | Ruta                             | Descripción                                      | Roles    |
|--------|----------------------------------|--------------------------------------------------|----------|
| GET    | /api/admin/users                 | Listar todos los usuarios                       | ADMIN    |
| POST   | /api/admin/users                 | Crear usuario                                    | ADMIN    |
| GET    | /api/admin/users/:id             | Ver detalle de usuario                           | ADMIN    |
| PUT    | /api/admin/users/:id             | Editar usuario                                   | ADMIN    |
| DELETE | /api/admin/users/:id             | Eliminar usuario                                 | ADMIN    |
| PUT    | /api/admin/users/:id/status      | Cambiar estado del usuario                       | ADMIN    |
| PUT    | /api/admin/users/:id/role        | Cambiar rol del usuario                          | ADMIN    |
| GET    | /api/admin/courses               | Listar todos los cursos                          | ADMIN    |
| PUT    | /api/admin/courses/:id/status    | Cambiar estado del curso                         | ADMIN    |
| GET    | /api/admin/categories            | Gestionar categorías                             | ADMIN    |
| POST   | /api/admin/categories            | Crear categoría                                  | ADMIN    |
| PUT    | /api/admin/categories/:id        | Editar categoría                                 | ADMIN    |
| DELETE | /api/admin/categories/:id        | Eliminar categoría                               | ADMIN    |
| GET    | /api/admin/membership-plans      | Gestionar planes de membresía                    | ADMIN    |
| POST   | /api/admin/membership-plans      | Crear plan de membresía                          | ADMIN    |
| PUT    | /api/admin/membership-plans/:id  | Editar plan                                      | ADMIN    |
| DELETE | /api/admin/membership-plans/:id  | Eliminar plan                                    | ADMIN    |
| GET    | /api/admin/payments              | Ver todos los pagos                              | ADMIN    |
| GET    | /api/admin/enrollments           | Ver todas las inscripciones                      | ADMIN    |
| GET    | /api/admin/reviews               | Moderar reseñas de cursos                        | ADMIN    |
| PUT    | /api/admin/reviews/:id/approve   | Aprobar reseña                                   | ADMIN    |
| PUT    | /api/admin/reviews/:id/reject    | Rechazar reseña                                  | ADMIN    |
| DELETE | /api/admin/reviews/:id           | Eliminar reseña                                  | ADMIN    |
| GET    | /api/admin/certificates          | Listar todos los certificados                    | ADMIN    |
| GET    | /api/admin/analytics             | Dashboard completo de analíticas                 | ADMIN    |
| GET    | /api/admin/site-settings         | Ver configuración del sitio                      | ADMIN    |
| PUT    | /api/admin/site-settings         | Actualizar configuración                         | ADMIN    |

---

## Rutas de notificaciones

| Método | Ruta                             | Descripción                                      | Roles    |
|--------|----------------------------------|--------------------------------------------------|----------|
| GET    | /api/notifications               | Listar notificaciones del usuario               | Usuarios |
| PUT    | /api/notifications/:id/read      | Marcar notificación como leída                   | Usuarios |
| PUT    | /api/notifications/read-all      | Marcar todas como leídas                         | Usuarios |
| DELETE | /api/notifications/:id           | Eliminar notificación                            | Usuarios |

---

## Rutas de archivos multimedia

| Método | Ruta                             | Descripción                                      | Roles               |
|--------|----------------------------------|--------------------------------------------------|---------------------|
| POST   | /api/media/upload                | Subir archivo multimedia                         | INSTRUCTOR, ADMIN   |
| GET    | /api/media/:id                   | Descargar/ver archivo                            | Usuarios            |
| DELETE | /api/media/:id                   | Eliminar archivo                                 | INSTRUCTOR, ADMIN   |

---

## Notas de seguridad y buenas prácticas

- **Autenticación JWT:** Refresh tokens, expiración configurable, blacklist de tokens.
- **Rate limiting:** Protección contra abuso en endpoints críticos.
- **Validación:** Sanitización de datos de entrada, validación de esquemas.
- **Autorización:** Control granular por roles y propiedad de recursos.
- **Pagos seguros:** Integración completa con Stripe, manejo de webhooks.
- **Logging:** Auditoría completa de acciones administrativas y transacciones.
- **CORS y Headers:** Configuración segura para producción.
- **Prevención:** XSS, CSRF, SQL Injection, y ataques de enumeración.

---