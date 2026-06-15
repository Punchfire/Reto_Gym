# Reto del Gimnasio — Tracker

App estática de un solo archivo (`index.html`) para llevar el control del reto.

## Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub (puede ser público o privado, aunque para Pages gratis se recomienda público).
2. Sube el archivo `index.html` a la raíz del repositorio.
3. Ve a **Settings → Pages**.
4. En "Source" elige **Deploy from a branch**, selecciona la rama `main` y la carpeta `/ (root)`.
5. Guarda. En unos minutos tu app estará disponible en:
   `https://<tu-usuario>.github.io/<nombre-del-repo>/`

## Datos compartidos entre las dos personas (recomendado)

Por defecto, sin configuración adicional, la app guarda los datos en el
`localStorage` del navegador, es decir **cada persona ve solo lo que registra
en su propio dispositivo**.

Para que ambos vean el mismo calendario, gráfica y registros desde cualquier
dispositivo, conecta una base de datos gratuita con Firebase:

1. Ve a https://console.firebase.google.com y crea un proyecto nuevo (gratis).
2. En el menú lateral, entra a **Build → Firestore Database** y crea una
   base de datos en **modo de prueba** (test mode).
3. Ve a **Project settings → General**, baja hasta "Your apps", crea una
   app web (icono `</>`) y copia el objeto de configuración que se ve así:
   ```js
   const firebaseConfig = {
     apiKey: "...",
     authDomain: "...",
     projectId: "...",
     storageBucket: "...",
     messagingSenderId: "...",
     appId: "..."
   };
   ```
4. Abre `index.html`, busca la constante `FIREBASE_CONFIG` (cerca del inicio
   del `<script type="module">`) y pega ahí tus valores.
5. Sube el archivo actualizado al repositorio. La app detectará la
   configuración y sincronizará los datos automáticamente entre ambos.

### Nota sobre seguridad
El "modo de prueba" de Firestore deja la base de datos abierta durante 30
días (cualquiera con la URL podría leer/escribir). Para un proyecto personal
entre dos personas esto suele ser aceptable, pero si quieres más seguridad,
puedes ajustar las reglas de Firestore para restringir el acceso (por
ejemplo, exigiendo autenticación).

## Funcionalidad

- Registro de entrenamientos: persona, fecha, hora, duración y foto
  (se comprime automáticamente antes de guardarse).
- Marcador con días y semanas restantes del reto.
- Gráfica de asistencias semanales por persona, con línea de meta en 3.
- Calendario mensual con marcas de color por persona.
- Lista de últimos registros, con opción de borrar.
- Configuración de nombres y fechas de inicio/fin desde el ícono de engranaje.
