## Tips de seguridad

### 1. Firmar con certificados de producción:

- Nunca publiques aplicaciones firmadas con certificados de depuración. Asegúrate de firmarlas con un certificado de producción adecuado. 
Las aplicaciones firmadas con certificados de depuración son más vulnerables a la manipulación.
- **Tip:** Establece un flujo de integración continua (CI/CD) para firmar automáticamente las versiones de producción con certificados válidos y evitar errores manuales.
