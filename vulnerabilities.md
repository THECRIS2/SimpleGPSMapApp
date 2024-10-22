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
- **Impacto:** Los certificados de depuración no deben utilizarse en aplicaciones de producción porque están diseñados para uso en desarrollo. Un atacante podría explotar esta vulnerabilidad para inyectar código malicioso o modificar la aplicación. 
- **Pasos de reproduccion:**
  1. Instalar la aplicación en un dispositivo o emulador.
  2. Navegar a la configuración del dispositivo y habilitar las opciones de desarrollador.
  3. Verificar la firma de la aplicación mediante un comando como apksigner verify --verbose --print-certs app.apk.
- **Correcciones:**
  1. Firmar la aplicación con un certificado de producción antes de publicarla.
  2. Verificar que no se utilice el certificado de depuración al generar builds de producción.

### 2. Aplicación vulnerable a la vulnerabilidad Janus
- **Descripcion:** La aplicación está firmada con el esquema de firma v1, lo que la hace vulnerable a la vulnerabilidad Janus en Android 5.0-8.0, si está firmada solo con el esquema de firma v1. Las aplicaciones que se ejecutan en Android 5.0-7.0 firmadas con el esquema v1 y v2/v3 también son vulnerables.
- **Gravedad:** Media
- **Impacto:** La vulnerabilidad Janus permite modificar aplicaciones APK sin romper las firmas v1, lo que posibilita la inyección de código malicioso en aplicaciones firmadas solo con el esquema de firma v1. Afecta principalmente a versiones de Android 5.0 a 8.0
- **Pasos de reproduccion:**
  1. Verificar que la aplicación esté firmada únicamente con el esquema v1 usando apksigner verify --verbose app.apk.
  2. Revisar si la aplicación puede ser manipulada para agregar código sin romper la firma
- **Correcciones:**
  1. Firmar la aplicación usando el esquema de firma v2 o superior para evitar la vulnerabilidad.
  2. Mantener el esquema de firma v1 para compatibilidad, pero añadir el esquema v2 y v3

### 3. La aplicacion se puede instalar en una version de android obsoleta 6.0-6.0.1, [minSdk=23]
- **Descripcion:** Esta aplicación se puede instalar en una versión anterior de Android que tenga múltiples vulnerabilidades sin corregir. Estos dispositivos no recibirán actualizaciones de seguridad razonables de Google. Admite una versión de Android => 10, API 29 para recibir actualizaciones de seguridad razonables.
- **Gravedad:** Alta
- **Impacto:** Las versiones obsoletas de Android, como la 6.0, no reciben actualizaciones de seguridad, exponiendo la aplicación a múltiples vulnerabilidades críticas. Esto incluye posibles ataques mediante exploits conocidos y sin parchear
- **Pasos de reproduccion:**
  1. Instalar la aplicación en un dispositivo con Android 6.0 o 6.0.1.
  2. Verificar si la aplicación funciona en un entorno vulnerable, utilizando un dispositivo antiguo.
- **Correcciones:**
  1. Incrementar la minSdkVersion en el archivo build.gradle a una versión que aún reciba actualizaciones de seguridad, como API 29 (Android 10) o superior.
  2. Realizar pruebas de compatibilidad con las versiones de Android actualizadas.

### 4. Depuración habilitada para la aplicación [android:debuggable=true]
- **Descripcion:** Se habilitó la depuración en la aplicación, lo que facilita que los ingenieros inversos conecten un depurador a ella. Esto permite volcar un seguimiento de la pila y acceder a las clases auxiliares de depuración.
- **Gravedad:** Alta
- **Impacto:** Permitir la depuración en una aplicación en producción facilita a los atacantes el uso de herramientas para inspeccionar o modificar el código. Esto puede comprometer la integridad de la aplicación y la seguridad del usuario.
- **Pasos de reproduccion:**
  1. Instalar la aplicación.
  2. Conectar el dispositivo a un entorno de depuración y ejecutar el comando adb shell ps para ver si la aplicación está en modo de depuración.
  3. Intentar adjuntar un depurador y realizar inspección de la aplicación en ejecución.
- **Correcciones:**
  1. Deshabilitar la depuración en la versión de producción cambiando android:debuggable=false en el archivo     AndroidManifest.xml.
  2. Asegurarse de que las compilaciones de producción no incluyan banderas de depuración.

### 5. Se pueden realizar copias de seguridad de los datos de la aplicación [android:allowBackup=true]
- **Descripcion:** Esta bandera permite que cualquier persona haga una copia de seguridad de los datos de su aplicación a través de adb. Permite que los usuarios que hayan habilitado la depuración USB copien los datos de la aplicación fuera del dispositivo.
- **Gravedad:** Media
- **Impacto:** Permitir la copia de seguridad de los datos de la aplicación expone información sensible si se habilita la depuración USB. Un atacante podría obtener copias de seguridad de datos confidenciales.
- **Pasos de reproduccion:**
  1. Conectar el dispositivo a un ordenador con adb habilitado.
  2. Ejecutar el comando adb backup -f backup.ab -apk -obb package_name.
  3. Verificar si se realiza correctamente una copia de seguridad de la aplicación.
- **Correcciones:**
  1. Deshabilitar la opción de copia de seguridad de datos añadiendo android:allowBackup=false en el archivo   AndroidManifest.xml.
  2. Implementar cifrado para los datos sensibles que se almacenan localmente.

### 6. El receptor de transmisión (androidx.profileinstaller.ProfileInstallReceiver) está protegido por un permiso, pero se debe verificar el nivel de protección del permiso. Permiso: android.permission.DUMP [android:exported=true]
- **Descripcion:** Se ha descubierto que un receptor de transmisión se comparte con otras aplicaciones del dispositivo, por lo que queda accesible para cualquier otra aplicación del dispositivo. Está protegido por un permiso que no está definido en la aplicación analizada. Como resultado, se debe comprobar el nivel de protección del permiso en el lugar donde esté definido. Si se configura como normal o peligroso, una aplicación maliciosa puede solicitar y obtener el permiso e interactuar con el componente. Si se configura como de firma, solo las aplicaciones firmadas con el mismo certificado pueden obtener el permiso.
- **Gravedad:** Media
- **Impacto:** Un receptor de transmisión que esté expuesto públicamente y protegido por un permiso mal configurado puede permitir que aplicaciones maliciosas interactúen con el componente. Esto podría usarse para manipular el comportamiento de la aplicación.
- **Pasos de reproduccion:**
  1. Revisar el archivo AndroidManifest.xml y localizar el receptor de transmisión.
  2. Verificar que el permiso android.permission.DUMP esté correctamente configurado.
  3. Crear una aplicación que intente interactuar con el receptor de transmisión sin tener el permiso adecuado.
- **Correcciones:**
  1. Revisar el nivel de protección del permiso para asegurarse de que sea adecuado (debería ser de tipo signature para limitar el acceso a aplicaciones firmadas con el mismo certificado).
  2. Cambiar android:exported a false si el componente no necesita ser accesible desde otras aplicaciones.
