# GPSMapApp

## Descripción

El proyecto es una aplicación Android que permite el uso de GPS para localizar usuarios. A continuaicón se realiza una auditoría de seguridad para identificar vulnerabilidades y proponer mejoras en su seguridad.

## Vulnerabilidades Identificadas

- **Certificado de Depuración**: La aplicación está firmada con un certificado de depuración, lo cual no es seguro para entornos de producción.
- **Depuración Habilitada**: El flag `android:debuggable=true` está activo, lo que facilita el trabajo de ingeniería inversa.
- **Permiso para Respaldo**: El flag `android:allowBackup=true` permite realizar respaldos de datos de la app, exponiendo información sensible si se habilita el modo depuración en el dispositivo.
- **Receivers Exportados**: Un Broadcast Receiver está expuesto a otras aplicaciones y no tiene un nivel adecuado de protección.
- **Clave de Google Maps Hardcodeada**: Se identificó una clave de API de Google Maps dentro del código.

## Mejoras Implementadas

- **Deshabilitar Depuración**: Eliminar el flag `android:debuggable=true` en el archivo `AndroidManifest.xml` para evitar la ingeniería inversa.
- **Firmar con Certificado de Producción**: Firmar la aplicación con un certificado válido para entornos de producción.
- **Deshabilitar Respaldo de Datos**: Establecer `android:allowBackup=false` para prevenir que la información de la app sea copiada.
- **Proteger Broadcast Receiver**: Reforzar los permisos asociados a los componentes exportados para evitar que aplicaciones maliciosas interactúen con ellos.
- **Almacenar Claves de API de Forma Segura**: Mover la clave de la API de Google Maps a un servicio de gestión de secretos o variables de entorno.

## Buenas Prácticas de Seguridad

1. **Cifrado de Datos Sensibles**: Usar cifrado AES para proteger cualquier dato almacenado localmente que pueda ser sensible.
2. **Revisión de Permisos**: Solicitar solo los permisos estrictamente necesarios y revisar aquellos que puedan ser peligrosos, como los relacionados con la ubicación.
3. **Comunicación Segura**: Asegurar todas las comunicaciones utilizando HTTPS con certificados válidos.
4. **Gestión de Claves**: No almacenar claves de API directamente en el código fuente. Usar servicios de gestión de secretos o variables de entorno.
5. **Proteger Componentes Exportados**: Asegurarse de que los componentes de la aplicación que son exportados tengan permisos estrictos para evitar accesos no autorizados.

## Cómo Ejecutar la Aplicación de Forma Segura

1. Clonar el repositorio.
2. Importar el proyecto en Android Studio.
3. Asegurarse de que el entorno de desarrollo esté configurado para usar un certificado de producción.
4. Desactivar el flag `android:debuggable=true` en el archivo `AndroidManifest.xml`.
5. Ejecutar la aplicación en un dispositivo o emulador con las configuraciones de seguridad adecuadas.

## Reporte de Vulnerabilidades

El reporte detallado de las pruebas de vulnerabilidad realizadas se encuentra en el archivo `vulnerability_report.pdf`.
