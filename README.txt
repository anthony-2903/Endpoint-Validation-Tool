ENDPOINT READINESS SCANNER v1.0.0

PROPÓSITO
Scanner local, sin remediación, para que personal N2 valide cinco controles críticos antes de entregar un equipo Windows: Administradores locales, BitLocker, agentes de seguridad, software base y Windows/KB.

REQUISITOS Y EJECUCIÓN
- Windows con .NET Framework 4.x (incluido en Windows 10 y Windows 11).
- Ejecute EndpointReadinessScanner.exe. Es una aplicación de escritorio; no utiliza PowerShell.
- EndpointReadinessScanner.cmd es un lanzador opcional del ejecutable.
- El ejecutable solicita permisos administrativos mediante UAC al iniciarse. Acéptelos para realizar la validación completa.
- No se instala software ni se modifica la configuración del equipo.

CONFIGURACIÓN DEL BASELINE
Edite Baseline.json antes de uso productivo. Defina los miembros autorizados de Administradores locales, los agentes y servicios requeridos, el software obligatorio y las reglas de Windows/KB. La plantilla incluye Google Chrome y Adobe Acrobat como software requerido. Ajuste MinimumVersion a la versión mínima aprobada por su organización; el scanner compara la versión instalada con ese valor. Los arreglos vacíos de la plantilla se reportan como ADVERTENCIA y, al ser controles críticos, impiden aprobar el equipo. Los nombres de miembros deben coincidir con los devueltos por Windows, por ejemplo DOMINIO\AdminIT.

RESULTADOS
Los estados son OK, FALLA, ADVERTENCIA y NO EVALUADO. La lista muestra un icono: ✓ para OK, ✕ para FALLA, ! para ADVERTENCIA y ? para NO EVALUADO. Seleccione un control de la lista para ver lo esperado, lo detectado, el motivo y la acción necesaria. El resultado final es APTO PARA ENTREGA únicamente cuando los cinco controles críticos tienen estado OK. El scanner nunca corrige configuraciones ni expone claves BitLocker.

EVIDENCIA Y REGISTROS
Al terminar se crea Evidence\YYYY\MM\SERIAL_YYYYMMDD_HHMMSS\ con Resultado.json, Resumen.txt y Auditoria.log. Los mensajes técnicos se almacenan en Logs\Scanner.log.

ESTRUCTURA
EndpointReadinessScanner.exe  Aplicación gráfica de escritorio
EndpointReadinessScanner.cs  Código fuente de la aplicación
Baseline.json  Estándar configurable
Evidence\  Evidencia generada automáticamente
Logs\  Registro técnico

LIMITACIONES V1
No incluye remediación, TPM, Secure Boot, hardware, VPN, red, perfiles, tickets ni integración con ServiceDesk. La comparación de software usa las claves de desinstalación de Windows; ciertos instaladores portables pueden no aparecer allí.
