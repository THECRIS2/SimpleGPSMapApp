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
-**Descripcion:** La aplicación está firmada con el esquema de firma v1, lo que la hace vulnerable a la vulnerabilidad Janus en Android 5.0-8.0, si está firmada solo con el esquema de firma v1. Las aplicaciones que se ejecutan en Android 5.0-7.0 firmadas con el esquema v1 y v2/v3 también son vulnerables.

