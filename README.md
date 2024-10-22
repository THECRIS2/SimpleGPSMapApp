# SimpleGPSMapApp #
# Descripción
Este proyecto es una aplicación Android que implementa medidas de seguridad para proteger
contra vulnerabilidades comunes.
## Vulnerabilidades Identificadas
- Certificado de depuracion
- Vulnerable a la vulnerabilidad Janus
- Aplicacion que usa una version obsoleta de android
- Depuracion habilitada para la app
- Se pueden realizar copias de seguridad no autorizadas
- Verificacion del nivel de proteccion del permiso
## Mejoras Implementadas
- Desactivacion de depuracion
- Eliminar vulnerabilidad Janus
- Actualizacion sdk para admitir de android 10+
- Solo poder realizar copias de seguridad por personal autorizado
- Eliminar certificado de depuracion
- Nivel de proteccion del permiso del gps adecuado
## Documentación
- [Vulnerabilidades](vulnerabilities.md)
- [Best Practices](best_practices.md)
- [Security Tips](security_tips.md)
- [Security Improvement Program](security_improvement_program.md)
## Cómo Ejecutar la Aplicación de Forma Segura
1. Clonar el repositorio git clone https://github.com/THECRIS2/SimpleGPSMapApp.git
2. Importar el proyecto en Android Studio
3. Ejecutar la aplicación en un dispositivo o emulador
4. Asegurarse de que los permisos necesarios están configurados
## Reporte de Vulnerabilidades El reporte detallado de las pruebas de vulnerabilidad
El informe de las vulnerabilidades encontradas se encuentra en el archivo `vulnerability_report.pdf`.
