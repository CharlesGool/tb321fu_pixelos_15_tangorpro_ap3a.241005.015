# tb321fu_pixelos_15_tangorpro_ap3a.241005.015

[简体中文](../../README.md) | [English](../en/README.md) | **Español**

Paquete de flasheo 9008 para la Lenovo Legion Y700 de tercera generación (TB321FU) con el GSI de Android 15 de Pixel Tablet (`AP3A.241005.015`).

[![Release](https://img.shields.io/github/v/release/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015?logo=github)](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest)

## Documentación

- Descripción general del proyecto: [README](README.md)

- Justificación del diseño: [DESIGN](DESIGN.md)

- Estado del proyecto: [LOG](LOG.md)
- Registros históricos: [HISTORY](HISTORY.md)
- Historial de cambios: [CHANGELOG](CHANGELOG.md)

- Avisos de terceros: [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md)

## Introducción

En el TB321FU, el GSI de Android 15 de Pixel Tablet (`tangorpro`) reemplaza a ZUI y añade las funciones y correcciones que al GSI le faltan en este equipo. La base es el `AP3A.241005.015` de Mystic GSI, y vendor y boot son los de ZUI 17.0.12 originales de Lenovo.

La versión oficial actual, user-v1.2 (versión interna V129), incluye:

- Sistema Pixel, con la identidad restaurada al modelo original y que supera la verificación de integridad de Play.
- Desbloqueo facial, rotación libre, ocultación de la barra de navegación y niveles de fluidez de pantalla (hasta 165Hz).
- Correcciones de hardware: audio por Bluetooth, punto de acceso de 6GHz, brillo automático, tasa de refresco adaptativa, cámara macro, etc.
- Compatibilidad con aplicaciones de 32 bits y cámara de Pixel.
- `herald-core`: punto de entrada de comandos y complementos del sistema.

La lista de módulos está en [modules-user-v1.2](../modules-user-v1.2.md). Los parches y el sistema de compilación están en [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro tiene varias versiones de base; cada una tiene su propio repositorio, y este solo corresponde a `AP3A.241005.015`.

## Requisitos

- Lenovo Legion Y700 de tercera generación TB321FU, capaz de entrar en el modo 9008 (EDL).
- PC con Windows, cable USB y 7-Zip.
- El flasheo conservando datos solo se aplica si el dispositivo ya tenía este sistema del proyecto; en los demás casos, use el flasheo con borrado de datos.

## Instalación

### Instalación rápida

Descargue todos los volúmenes (`.7z.001`, `.7z.002`) desde [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) y colóquelos en el mismo directorio. Descomprima `.7z.001` con 7-Zip. Con el dispositivo en modo 9008, ejecute `flash.bat` en el directorio descomprimido (borra los datos).

### Instalación normal

```bash
sha256sum -c SHA256SUMS.txt
7z x pixelos_tangorpro_ap3a.241005.015_user-v1.2_optional.7z.001
```

Para flashear conservando datos, ejecute `flash_keep_data.bat`. Ambos scripts están en la raíz del directorio descomprimido.

## Guía

| Archivo | Contenido |
| --- | --- |
| `…user-v1.2_optional.7z.001`, `.002` | Volúmenes 7z del paquete completo de flasheo 9008, de 2000 MiB cada uno |
| `SHA256SUMS.txt` | Sumas de verificación de los volúmenes; el sha256 de los dos volúmenes concatenados en orden es `4cc450d58ef89097fe3a4b07b5aa53d01032e390371208e002aeb985fabe6cf2` |
| `module-list.md` | Lista de módulos de esta versión, igual que [modules-user-v1.2](../modules-user-v1.2.md) |

Identificación de versión: la versión pública es `user-vMAJOR.MINOR`; el número interno `V<número>` está escrito en la imagen. user-v1.2 = V129.

## Actualización

Por ahora no hay.

## Desinstalación

No hay un método separado para la desinstalación rápida. Desinstalación completa: vuelva a flashear el paquete 9008 del ZUI 17.0.12 original de Lenovo; los datos se borrarán.

## Agradecimientos

- El GSI de Pixel Tablet de Mystic GSI como base del sistema.
- El motor de certificación es una bifurcación de [ITxiao6666/OhMyKeymint](https://github.com/ITxiao6666/OhMyKeymint) (autor original: James Clef / qwq233).
- El firmware original de ZUI y las herramientas de flasheo de Lenovo.

Los datos de autoría y de cumplimiento están en [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).

## Licencia

Este repositorio todavía no ha elegido una licencia y no concede ninguna. El estado de licencia de cada componente de terceros está en [THIRD_PARTY_NOTICES](THIRD_PARTY_NOTICES.md).
