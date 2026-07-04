# Cumplimiento y seguridad

Aviso: guia practica, no asesoramiento juridico. Con datos personales o regulados,
revisar el despliegue con un profesional antes de escalar.

## RGPD y datos
- Base legal clara para el tratamiento y aviso de privacidad.
- Acuerdo de tratamiento (DPA) con los proveedores implicados.
- Compromiso contractual de **no entrenar** modelos con tus datos.
- Minimizacion: solo los datos necesarios, el tiempo necesario.

## Seguridad del sistema
- **Control de acceso por documento (ACLs)** respetado en la recuperacion: un comercial
  no accede a nominas aunque esten en el mismo sistema. Nunca "un unico saco" sin control.
- Registro de auditoria de preguntas y fuentes.
- Cifrado en transito y en reposo.
- Opcion on-premise para datos que no pueden salir de la infraestructura.

## Marco
RGPD (UE 2016/679), LOPDGDD (LO 3/2018) y buenas practicas de seguridad para sistemas
de IA empresarial.
