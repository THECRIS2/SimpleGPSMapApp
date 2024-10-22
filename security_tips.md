## Tips de seguridad

### 1. Firmar con certificados de producción:

- Nunca publiques aplicaciones firmadas con certificados de depuración. Asegúrate de firmarlas con un certificado de producción adecuado. 
Las aplicaciones firmadas con certificados de depuración son más vulnerables a la manipulación.
- **Tip:** Establece un flujo de integración continua (CI/CD) para firmar automáticamente las versiones de producción con certificados válidos y evitar errores manuales.

### 2. Utilizar esquemas de firma v2/v3:

- Actualiza el esquema de firma de la aplicación a v2 o v3 para asegurar la integridad de las aplicaciones, ya que las versiones v1 son vulnerables a ataques como la vulnerabilidad Janus.
- **Tip:** Configura tu build.gradle para firmar con esquemas múltiples (v1, v2, v3) y así garantizar compatibilidad con dispositivos antiguos sin comprometer la seguridad.

### 3. Configurar correctamente el minSdkVersion:

- Evita soportar versiones de Android que ya no reciben actualizaciones de seguridad. Las versiones antiguas son más propensas a vulnerabilidades conocidas.
- **Tip:** Actualiza regularmente la API mínima (por ejemplo, API 29 o superior) para asegurarte de que tu aplicación funcione solo en dispositivos con parches de seguridad actualizados.

### 4. Deshabilitar la depuración en producción:

- Asegúrate de que el atributo android:debuggable esté configurado en false en las versiones de producción. Dejar la depuración habilitada permite que atacantes utilicen herramientas de ingeniería inversa para explotar tu aplicación.
- **Tip:** Crea perfiles de compilación separados para debug y release, con configuraciones específicas para cada entorno, desactivando depuración y otras herramientas de desarrollo en producción.

### 5. Desactivar las copias de seguridad de datos sensibles:

- Si tu aplicación maneja datos sensibles, desactiva la posibilidad de hacer copias de seguridad automáticas mediante el atributo android:allowBackup="false".
- **Tip:** Usa encriptación para cualquier dato sensible almacenado localmente y verifica regularmente el uso de permisos críticos como la copia de seguridad.

### 6. Protege los receptores de transmisión (Broadcast Receivers):

- Si tienes receptores de transmisión (Broadcast Receivers) exportados a otras aplicaciones, asegúrate de que estén protegidos con permisos fuertes (por ejemplo, signature). No uses permisos con niveles de protección débiles como normal o dangerous sin una necesidad justificada.
- **Tip:** Si el componente no necesita interactuar con otras aplicaciones, configúralo con android:exported="false" para evitar la exposición innecesaria.

### 7. Revisa los permisos de la aplicación regularmente:

- Verifica que tu aplicación solo solicite los permisos estrictamente necesarios para su funcionamiento. Permisos excesivos pueden aumentar la superficie de ataque.
- **Tip:** Realiza auditorías regulares de los permisos y usa mecanismos como permisos en tiempo de ejecución para garantizar que los usuarios otorguen acceso solo cuando sea absolutamente necesario.

### 8. Implementa políticas de seguridad fuertes:

- Usa ProGuard o R8 para ofuscar el código de tu aplicación, haciendo más difícil que los atacantes analicen el código fuente mediante técnicas de ingeniería inversa.
- **Tip:** Asegúrate de que las reglas de ProGuard estén correctamente configuradas para no eliminar o proteger clases críticas, como los manejadores de excepciones.

### 9. Manejo adecuado de permisos y componentes exportados:

- Revisa el atributo android:exported en tu AndroidManifest.xml para asegurarte de que no estés exponiendo servicios, actividades o receptores a aplicaciones de terceros sin una protección adecuada.
- **Tip:** Para componentes expuestos que requieren permisos, usa permisos del tipo signature para que solo las aplicaciones firmadas con el mismo certificado puedan interactuar con esos componentes.

## 10. Mantener dependencias actualizadas:

- Muchas vulnerabilidades provienen de librerías de terceros desactualizadas. Revisa y actualiza regularmente las dependencias de tu proyecto.
- **Tip:** Usa herramientas como Dependabot o Renovate que te notifiquen automáticamente de actualizaciones y posibles vulnerabilidades en tus dependencias.
