---
name: project-changelog-es
description: Historial de cambios
metadata:
  version: "1.0.0"
  lang: "es"
---

# Historial de cambios

## Multilingüe

[简体中文](../CHANGELOG.md) | [English](../en/CHANGELOG.md) | **Español**

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Historial de cambios

### user-v1.3(V132)- 2026-11-04

- Añadido: segunda Release de este repositorio, con un parche para actualizar de user-v1.2 conservando datos (14MB).
- Cambiado: `herald-core` pasa a V1.3, el directorio de trabajo vuelve a `/data/local/tmp` y se corrige el problema de etiquetas SELinux de V1.2 detectado en el dispositivo real.
- Cambiado: el motor de certificación pasa a una compilación nueva con endurecimiento de seguridad: las versiones desconocidas no provocan un panic, `keymint.dat` se escribe de forma atómica y un fallo al analizar el keybox no sobrescribe los archivos existentes.

### user-v1.2(V129)- 2026-11-04

- Añadido: primera Release de este repositorio, con las partes completas del paquete de flasheo 9008, `SHA256SUMS.txt` y la lista de módulos.
- Corregido: Bluetooth. `vendor-bind` añade `mounton` y la lectura de `vendor_file` en el dominio `update_engine`, de modo que los bind de la política de audio Bluetooth y de SCO surtan efecto en modo Enforcing.
