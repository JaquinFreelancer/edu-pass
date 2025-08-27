# 🗺️ Mapa de rutas Frontend

> **Comentarios:**  
> - Este mapa define las rutas principales de la interfaz web para la plataforma de cursos online y membresías.
> - Se basa en la estructura y entidades del ERD proporcionado y las mejores prácticas de UX, SEO y seguridad.
> - Indica si la ruta es pública, requiere autenticación, o es solo para roles específicos (ADMIN, INSTRUCTOR, STUDENT).
> - El frontend debe consumir la API backend siguiendo el mapa anterior.

---

## Rutas públicas (accesibles para cualquier visitante)

| Ruta                       | Página/Componente                | Descripción                                         |
|----------------------------|----------------------------------|-----------------------------------------------------|
| `/`                        | HomePage                         | Página principal, planes, cursos destacados, testimonios |
| `/cursos`                  | CoursesList                      | Listado de cursos con filtros y búsqueda            |
| `/cursos/categoria/:slug`  | CoursesByCategory                | Cursos por categoría específica                     |
| `/cursos/:slug`            | CourseDetail                     | Detalle del curso, previsualización, reseñas        |
| `/cursos/:slug/preview`    | CoursePreview                    | Lecciones de vista previa del curso                 |
| `/instructores`            | InstructorsList                  | Listado de instructores                             |
| `/instructores/:id`        | InstructorProfile                | Perfil público del instructor                       |
| `/planes`                  | MembershipPlans                  | Planes de membresía disponibles                     |
| `/sobre-nosotros`          | AboutUs                          | Información sobre la plataforma                     |
| `/contacto`                | Contact                          | Formulario de contacto                              |
| `/certificados/verificar`  | CertificateVerification          | Verificación de certificados                        |
| `/politica-privacidad`     | PrivacyPolicy                    | Política de privacidad                              |
| `/terminos-servicio`       | TermsOfService                   | Términos y condiciones                              |
| `/ayuda`                   | Help                             | Centro de ayuda y FAQ                               |
| `/buscar`                  | SearchResults                    | Resultados de búsqueda global                       |
| `/404`                     | NotFound                         | Página de error no encontrada                       |

---

## Rutas de autenticación y acceso

| Ruta                       | Página/Componente                | Descripción                                        | Acceso    |
|----------------------------|----------------------------------|----------------------------------------------------|-----------|
| `/login`                   | Login                            | Formulario de login                                | Pública   |
| `/registro`                | Register                         | Formulario de registro                             | Pública   |
| `/verificar-email`         | EmailVerification                | Verificación de email con token                    | Pública   |
| `/recuperar-password`      | PasswordReset                    | Solicitar recuperación de contraseña               | Pública   |
| `/restablecer-password/:token` | PasswordResetConfirm         | Formulario para restablecer contraseña             | Pública   |
| `/logout`                  | LogoutHandler                    | Acción de cierre de sesión                         | Usuarios  |

---

## Rutas del área de usuario (requieren autenticación)

| Ruta                       | Página/Componente                | Descripción                                        | Roles      |
|----------------------------|----------------------------------|----------------------------------------------------|------------|
| `/dashboard`               | UserDashboard                    | Dashboard principal del usuario                    | Usuarios   |
| `/perfil`                  | UserProfile                      | Editar perfil del usuario                          | Usuarios   |
| `/cambiar-password`        | ChangePassword                   | Cambiar contraseña                                 | Usuarios   |
| `/mis-cursos`              | MyCourses                        | Cursos en los que está inscrito                    | Usuarios   |
| `/curso/:slug/aprender`    | CoursePlayer                     | Reproductor del curso con lecciones                | Usuarios   |
| `/curso/:slug/modulo/:moduleId` | ModuleContent               | Contenido del módulo específico                    | Usuarios   |
| `/leccion/:id`             | LessonPlayer                     | Reproductor de lección individual                  | Usuarios   |
| `/quiz/:id`                | QuizPlayer                       | Interfaz para realizar quiz                        | Usuarios   |
| `/quiz/:id/resultados`     | QuizResults                      | Resultados del quiz realizado                      | Usuarios   |
| `/mi-progreso`             | ProgressOverview                 | Vista general del progreso en cursos               | Usuarios   |
| `/mis-certificados`        | MyCertificates                   | Certificados obtenidos                             | Usuarios   |
| `/certificado/:id`         | CertificateView                  | Vista y descarga de certificado                    | Usuarios   |
| `/mi-membresia`            | MyMembership                     | Estado y gestión de membresía                      | Usuarios   |
| `/suscribirse/:planId`     | MembershipCheckout               | Proceso de suscripción a plan                      | Usuarios   |
| `/comprar-curso/:slug`     | CourseCheckout                   | Proceso de compra de curso individual              | Usuarios   |
| `/pagos/exito`             | PaymentSuccess                   | Confirmación de pago exitoso                       | Usuarios   |
| `/pagos/error`             | PaymentError                     | Error en el proceso de pago                        | Usuarios   |
| `/historial-pagos`         | PaymentHistory                   | Historial de pagos realizados                      | Usuarios   |
| `/notificaciones`          | Notifications                    | Centro de notificaciones                           | Usuarios   |

---

## Rutas del área de instructor (INSTRUCTOR, ADMIN)

| Ruta                       | Página/Componente                | Descripción                                        | Roles              |
|----------------------------|----------------------------------|----------------------------------------------------|-------------------|
| `/instructor`              | InstructorDashboard              | Dashboard principal del instructor                 | INSTRUCTOR, ADMIN |
| `/instructor/cursos`       | InstructorCourses                | Gestión de cursos del instructor                   | INSTRUCTOR, ADMIN |
| `/instructor/cursos/nuevo` | CourseCreate                     | Crear nuevo curso                                  | INSTRUCTOR, ADMIN |
| `/instructor/cursos/:id/editar` | CourseEdit                  | Editar curso existente                             | INSTRUCTOR, ADMIN |
| `/instructor/cursos/:id/contenido` | CourseContentManagement    | Gestionar contenido del curso                      | INSTRUCTOR, ADMIN |
| `/instructor/modulos/nuevo` | ModuleCreate                    | Crear nuevo módulo                                 | INSTRUCTOR, ADMIN |
| `/instructor/modulos/:id/editar` | ModuleEdit                 | Editar módulo                                      | INSTRUCTOR, ADMIN |
| `/instructor/lecciones/nueva` | LessonCreate                  | Crear nueva lección                                | INSTRUCTOR, ADMIN |
| `/instructor/lecciones/:id/editar` | LessonEdit               | Editar lección                                     | INSTRUCTOR, ADMIN |
| `/instructor/quiz/nuevo`   | QuizCreate                       | Crear nuevo quiz                                   | INSTRUCTOR, ADMIN |
| `/instructor/quiz/:id/editar` | QuizEdit                      | Editar quiz existente                              | INSTRUCTOR, ADMIN |
| `/instructor/estudiantes`  | InstructorStudents               | Ver estudiantes de mis cursos                      | INSTRUCTOR, ADMIN |
| `/instructor/estudiantes/:id` | StudentProgress               | Ver progreso específico de estudiante              | INSTRUCTOR, ADMIN |
| `/instructor/recursos`     | MediaManager                     | Gestión de archivos multimedia                     | INSTRUCTOR, ADMIN |
| `/instructor/analytics`    | InstructorAnalytics              | Estadísticas y análisis de cursos                  | INSTRUCTOR, ADMIN |
| `/instructor/ingresos`     | InstructorEarnings               | Reporte de ingresos                                | INSTRUCTOR, ADMIN |

---

## Rutas administrativas (solo ADMIN)

| Ruta                       | Página/Componente                | Descripción                                        | Roles      |
|----------------------------|----------------------------------|----------------------------------------------------|------------|
| `/admin`                   | AdminDashboard                   | Panel principal de administración                  | ADMIN      |
| `/admin/usuarios`          | UserManagement                   | Gestión de usuarios del sistema                    | ADMIN      |
| `/admin/usuarios/nuevo`    | UserCreate                       | Crear nuevo usuario                                | ADMIN      |
| `/admin/usuarios/:id`      | UserEdit                         | Editar usuario específico                          | ADMIN      |
| `/admin/cursos`            | AdminCourseManagement            | Gestión de todos los cursos                        | ADMIN      |
| `/admin/cursos/:id/revisar` | CourseReview                    | Revisar y aprobar cursos                           | ADMIN      |
| `/admin/categorias`        | CategoryManagement               | Gestión de categorías de cursos                    | ADMIN      |
| `/admin/categorias/nueva`  | CategoryCreate                   | Crear nueva categoría                              | ADMIN      |
| `/admin/categorias/:id`    | CategoryEdit                     | Editar categoría                                   | ADMIN      |
| `/admin/planes`            | MembershipPlanManagement         | Gestión de planes de membresía                     | ADMIN      |
| `/admin/planes/nuevo`      | MembershipPlanCreate             | Crear nuevo plan                                   | ADMIN      |
| `/admin/planes/:id`        | MembershipPlanEdit               | Editar plan de membresía                           | ADMIN      |
| `/admin/membresias`        | MembershipManagement             | Gestión de membresías activas                      | ADMIN      |
| `/admin/pagos`             | PaymentManagement                | Gestión de pagos y transacciones                   | ADMIN      |
| `/admin/inscripciones`     | EnrollmentManagement             | Gestión de inscripciones                           | ADMIN      |
| `/admin/resenas`           | ReviewModeration                 | Moderación de reseñas de cursos                    | ADMIN      |
| `/admin/certificados`      | CertificateManagement            | Gestión de certificados emitidos                   | ADMIN      |
| `/admin/notificaciones`    | NotificationManagement           | Envío masivo de notificaciones                     | ADMIN      |
| `/admin/configuracion`     | SiteSettings                     | Configuración general del sitio                    | ADMIN      |
| `/admin/analytics`         | AdminAnalytics                   | Dashboard completo de analíticas                   | ADMIN      |
| `/admin/reportes`          | ReportsCenter                    | Centro de reportes y exportaciones                 | ADMIN      |

---

## Rutas especiales y funcionales

| Ruta                       | Página/Componente                | Descripción                                        | Acceso     |
|----------------------------|----------------------------------|----------------------------------------------------|------------|
| `/embed/curso/:slug`       | CourseEmbed                      | Vista embebida del curso                           | Públicas   |
| `/embed/leccion/:id`       | LessonEmbed                      | Vista embebida de lección                          | Usuarios   |
| `/api-docs`                | APIDocumentation                 | Documentación de la API                            | ADMIN      |
| `/health`                  | HealthCheck                      | Estado del sistema                                 | Sistema    |

---

## Consideraciones y buenas prácticas

- **Protección de rutas:** Todas las rutas de usuario requieren autenticación JWT válida.
- **Autorización por roles:** Validación de permisos antes de renderizar componentes.
- **SEO optimizado:** Meta tags, títulos dinámicos y URLs amigables para rutas públicas.
- **Responsive design:** Todas las rutas deben ser accesibles desde dispositivos móviles.
- **Lazy loading:** Carga diferida de componentes para optimizar rendimiento.
- **Error handling:** Manejo centralizado de errores y redirecciones apropiadas.
- **Breadcrumbs:** Navegación contextual en áreas administrativas y de curso.
- **Progreso visual:** Indicadores de progreso en cursos y formularios largos.
- **Accesibilidad:** Cumplimiento de estándares WCAG para usuarios con discapacidades.
- **Analytics:** Tracking de eventos importantes para análisis de uso.

---