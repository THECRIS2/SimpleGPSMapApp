# Reporte de vulnerabilidades

## Resumen
- Vulnerabilidades encontradas en total: 6
- Criticas: 0
- Alta: 3
- Media: 3
- Baja: 0

## Detalles de las vulnerabilidades
### 1. Solicitud firmada con certificado de depuración
- **Descripcion:** Aplicación firmada con certificado de depuración. La aplicación de producción no debe enviarse con un certificado de depuración.
- **Gravedad:** Alta
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**

### 2. Aplicación vulnerable a la vulnerabilidad Janus
- **Descripcion:** La aplicación está firmada con el esquema de firma v1, lo que la hace vulnerable a la vulnerabilidad Janus en Android 5.0-8.0, si está firmada solo con el esquema de firma v1. Las aplicaciones que se ejecutan en Android 5.0-7.0 firmadas con el esquema v1 y v2/v3 también son vulnerables.
- **Gravedad:** Media
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**

### 3. La aplicacion se puede instalar en una version de android obsoleta 6.0-6.0.1, [minSdk=23]
- **Descripcion:** Esta aplicación se puede instalar en una versión anterior de Android que tenga múltiples vulnerabilidades sin corregir. Estos dispositivos no recibirán actualizaciones de seguridad razonables de Google. Admite una versión de Android => 10, API 29 para recibir actualizaciones de seguridad razonables.
- **Gravedad:** Alta
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**

### 4. Depuración habilitada para la aplicación [android:debuggable=true]
- **Descripcion:** Se habilitó la depuración en la aplicación, lo que facilita que los ingenieros inversos conecten un depurador a ella. Esto permite volcar un seguimiento de la pila y acceder a las clases auxiliares de depuración.
- **Gravedad:** Alta
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**

### 5. Se pueden realizar copias de seguridad de los datos de la aplicación [android:allowBackup=true]
- **Descripcion:** Esta bandera permite que cualquier persona haga una copia de seguridad de los datos de su aplicación a través de adb. Permite que los usuarios que hayan habilitado la depuración USB copien los datos de la aplicación fuera del dispositivo.
- **Gravedad:** Media
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**

### 6. El receptor de transmisión (androidx.profileinstaller.ProfileInstallReceiver) está protegido por un permiso, pero se debe verificar el nivel de protección del permiso. Permiso: android.permission.DUMP [android:exported=true]
- **Descripcion:** Se ha descubierto que un receptor de transmisión se comparte con otras aplicaciones del dispositivo, por lo que queda accesible para cualquier otra aplicación del dispositivo. Está protegido por un permiso que no está definido en la aplicación analizada. Como resultado, se debe comprobar el nivel de protección del permiso en el lugar donde esté definido. Si se configura como normal o peligroso, una aplicación maliciosa puede solicitar y obtener el permiso e interactuar con el componente. Si se configura como de firma, solo las aplicaciones firmadas con el mismo certificado pueden obtener el permiso.
- **Gravedad:** Media
- **Impacto:**
- **Pasos de reproduccion:**
- **Correcciones:**
