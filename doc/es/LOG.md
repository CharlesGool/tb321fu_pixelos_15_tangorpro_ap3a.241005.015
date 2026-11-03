---
name: project-log-es
description: Errores, limitaciones, decisiones y traspaso del proyecto
metadata:
  version: "1.0.0"
  lang: "es"
---

# Registro

## Multilingüe

[简体中文](../LOG.md) | [English](../en/LOG.md) | **Español**

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Registros

- [Registros históricos](HISTORY.md)
- [Historial de cambios](CHANGELOG.md)

## Errores

No hay errores confirmados.

## Limitaciones

- La imagen del sistema incluye una semilla de keybox de respaldo; caduca o queda invalidada si se revoca, y a partir de ese momento la autenticación de claves requiere que el usuario importe un keybox válido. La semilla incluida en user-v1.2 tiene validez hasta el 2026-11-10 (fuente: nota de mantenimiento del proyecto; no verificada en la imagen).
- El flasheo conservando datos solo se aplica si el dispositivo ya tenía el sistema de este proyecto.

## Decisiones

| Fecha | Decisión | Estado | Motivo |
| --- | --- | --- | --- |
| 2026-11-04 | Un repositorio por versión base | Aceptada | PixelOS 15 tangorpro tiene varias versiones base |
| 2026-11-04 | Los Release solo incluyen el paquete 9008, no variantes con root | Aceptada | Indicación del usuario |
| 2026-11-04 | Volúmenes 7z de 2000 MiB cada uno | Aceptada | Por debajo del límite de 2 GiB por archivo de GitHub |
| 2026-11-04 | Licencias de terceros sin verificar al hacer público el repositorio | Aceptada | El usuario pidió hacerlo público expresamente; la verificación queda como paso pendiente |

## Traspaso

Consulte el traspaso vigente en el [LOG.md en chino simplificado](../LOG.md#交接).
