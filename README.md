UEPROMA Aula Virtual — publicación en GitHub Pages
Interfaz educativa responsive para docentes y estudiantes. La creación de cuentas estudiantiles utiliza Firebase Authentication y exige verificar el correo mediante un enlace enviado a Gmail antes de permitir el acceso.
1. Configurar Firebase
Entra a https://console.firebase.google.com/ y crea un proyecto para UEPROMA.
En Authentication → Sign-in method, activa Email/Password.
En Authentication → Settings → Authorized domains, agrega el dominio donde publicarás la web, por ejemplo `TUUSUARIO.github.io`. Si usas un dominio personalizado, agrégalo también.
En Configuración del proyecto → General → Tus aplicaciones, registra una aplicación web y copia su configuración.
Abre `UEPROMA_Aula_Virtual_Prototipo.html` y busca `const firebaseConfig`. Sustituye `REEMPLAZAR_API_KEY`, `REEMPLAZAR_PROJECT_ID` y `REEMPLAZAR_APP_ID` por los valores reales de tu proyecto. No dejes los marcadores de ejemplo.
En Firebase Authentication, configura la plantilla Email address verification y el nombre del remitente. Revisa también la carpeta Spam durante las pruebas.
La configuración web de Firebase se incluye en el cliente por diseño. Protege los datos con reglas de seguridad y nunca incluyas claves privadas de servidor o cuentas de servicio en este repositorio.
2. Habilitar las cuentas docentes
Crea cada cuenta docente desde Firebase Console → Authentication → Add user.
Verifica el correo de la cuenta docente.
En el HTML, edita `TEACHER_EMAILS` y agrega únicamente los correos docentes autorizados.
Importante: la lista `TEACHER_EMAILS` sirve para controlar la interfaz de este prototipo, pero no es una autorización segura por sí sola: el código del navegador es visible y modificable. Antes de usar información real, implementa roles mediante custom claims o documentos de perfil protegidos y aplica reglas de seguridad en Firestore/Storage o un backend.
3. Publicar en GitHub Pages
Crea un repositorio en GitHub.
Sube el HTML y, si deseas, este README. Para que GitHub Pages lo abra como página principal, renombra el HTML a `index.html`.
Ve a Settings → Pages.
En Build and deployment, selecciona Deploy from a branch, elige `main` y la carpeta `/ (root)` y guarda.
Espera a que GitHub publique la URL y asegúrate de que el dominio esté agregado en Firebase → Authentication → Authorized domains.
4. Qué valida el correo
Comprueba que el formato sea `@gmail.com`.
Firebase envía un enlace de verificación al buzón.
La cuenta no puede entrar hasta que el usuario abra el enlace y Firebase marque `emailVerified` como verdadero.
Si no llega el mensaje, revisar Spam y usar Reenviar verificación de correo.
La verificación confirma que el usuario controla esa dirección en ese momento; no garantiza que la cuenta siga activa para siempre.
5. Límites que debes conocer antes del uso institucional
Esta entrega actualiza la interfaz y la autenticación, pero el contenido académico (actividades, entregas, métricas y parte del perfil) aún se guarda en `localStorage` del navegador. Por tanto, no se comparte automáticamente entre estudiantes y docentes ni entre dispositivos. Los archivos adjuntos tampoco se suben a un servidor. Para un aula virtual institucional real, conecta Firestore para datos compartidos, Firebase Storage para archivos y reglas de seguridad por rol/curso. No cargues información sensible de estudiantes hasta implementar esas protecciones.
