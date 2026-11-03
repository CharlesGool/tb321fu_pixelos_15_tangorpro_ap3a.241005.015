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

En el TB321FU, el GSI de Android 15 de Pixel Tablet (`tangorpro`) reemplaza a ZUI y añade las funciones y correcciones que al GSI le faltan en este equipo. Flashear directamente un GSI de la comunidad provoca problemas: el brillo automático no funciona, los auriculares Bluetooth no suenan, las llamadas por Bluetooth no se oyen, las aplicaciones que solo funcionan en horizontal aparecen con la orientación invertida y no hay desbloqueo facial; este proyecto corrige todo ello.

Sistema: Android 15 `AP3A.241005.015`, con estilo Pixel. La base es el Pixel Tablet (`tangorpro`) de Mystic GSI; vendor y boot son los de ZUI 17.0.12.044 originales de Lenovo. El paquete de flasheo es un 9008 completo, firmado, y no requiere desactivar la verificación de vbmeta.

Versión oficial actual: user-v1.2 (versión interna V129). Los problemas conocidos están en [LOG](LOG.md#limitaciones).

### Características de la ROM

- Identidad restaurada al modelo original TB321FU, depuración desactivada por defecto, sin rastros de GSI ni de máquina virtual, y SELinux en modo Enforcing al arrancar.
- Suplantación global de huella digital y autenticación de claves, para superar la verificación de integridad de Play.
- Desbloqueo facial: incluye ParanoidSense de PixelOS (SDK de Megvii), usa la cámara frontal y es biometría WEAK (Class 2).
- Rotación libre: las cuatro orientaciones rotan automáticamente, incluida la vertical invertida.
- Niveles de fluidez de pantalla: en Ajustes, con "Fluidez de pantalla" activada no hay límite (el panel llega a 165Hz); desactivada, 120Hz.
- Ocultar la barra de navegación (barra de navegación en modo teléfono, línea de gestos, barra de tareas de tablet), con `heraldctl` para activarlo o desactivarlo.
- Compatibilidad con aplicaciones de 32 bits (traducción binaria Tango) y cámara de Pixel incluida (Cámara de Google 4.4).
- `herald-core`: punto de entrada de comandos y complementos sin root; las aplicaciones de frontend lo usan para controlar funciones del sistema.

### Qué se corrigió

- Brillo automático: se restablece el interruptor de brillo adaptativo en Ajustes, se usan la curva y la velocidad de respuesta del brillo original de Lenovo, y el nivel mínimo manual vuelve al original.
- Auriculares Bluetooth sin sonido y llamadas por Bluetooth que no se oyen: se desactiva el offload A2DP por hardware y se usa la codificación por software del vendor; se añaden comprobaciones de la política de audio y de SCO. Se desactiva LE Audio, que no está disponible, y los auriculares de modo dual usan Bluetooth clásico.
- Aplicaciones que solo funcionan en horizontal (como la pantalla completa de B 站) con la orientación invertida: se corrige la orientación de pantalla y se quita el ajuste de orientación de la base de Pixel Tablet.
- Tasa de refresco adaptativa: se restauran los temporizadores de inactividad y de tacto originales y la detección de contenido (baja con la pantalla estática, sube al tocar, y en vídeo sigue la tasa de fotogramas).
- Punto de acceso WLAN: se restauran la entrada de Ajustes y el mosaico de ajustes rápidos; el punto de acceso de 6GHz funciona.
- Cámara macro: tras restaurar la propiedad, el HAL de la cámara vuelve a mostrar la cámara macro n.º 2.
- Ventana emergente al arrancar y bucle de fallos: se quita la ventana "Se ha producido un problema interno en el dispositivo" y se corrige el servicio de conexión de dispositivos, que fallaba cada 10 segundos.
- Reducción: se eliminan los componentes de Pixel sin hardware correspondiente en este equipo (base, emisión, UWB, huella lateral, luz intensa/UV, banda base, etc.), las aplicaciones exclusivas de Pixel, restos de VNDK antiguo y del GSI, y, con el nivel 3, la mayoría de aplicaciones de Google (incluidas las de accesibilidad como TalkBack); las que necesite, instálelas de nuevo.

La función de cada módulo está en [modules-user-v1.2](../modules-user-v1.2.md).

### Hardware compatible

Hardware cubierto por las correcciones anteriores: CPU/GPU, Bluetooth (auriculares y llamadas), Wi-Fi y punto de acceso WLAN (incluido 6GHz), brillo automático, alta tasa de refresco de 165Hz, cámaras frontal, trasera y macro, rotación automática y desbloqueo facial. Esta lista indica lo que cubren las correcciones; no hay registro de pruebas individuales para cada elemento.

Los parches y el sistema de compilación están en [TB321FU-GSI-Mods](https://github.com/CharlesGool/TB321FU-GSI-Mods). PixelOS 15 tangorpro tiene varias versiones de base; cada una tiene su propio repositorio, y este solo corresponde a `AP3A.241005.015`.

## Requisitos

- Lenovo Legion Y700 de tercera generación TB321FU, capaz de entrar en el modo 9008 (EDL).
- PC con Windows, cable USB y 7-Zip.
- El flasheo conservando datos solo se aplica si el dispositivo ya tenía este sistema del proyecto; en los demás casos, use el flasheo con borrado de datos.

## Instalación

### Instalación rápida

Descargue todos los volúmenes (`.7z.001`, `.7z.002`) desde [Releases](https://github.com/CharlesGool/tb321fu_pixelos_15_tangorpro_ap3a.241005.015/releases/latest) y colóquelos en el mismo directorio. Descomprima `.7z.001` con 7-Zip. Con el dispositivo en modo 9008, ejecute `flash.bat` en el directorio descomprimido (borra los datos). El paquete incluye el firmware 9008 completo de Lenovo; no hace falta flashear antes un firmware oficial.

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

### Uso del desbloqueo facial

Ajustes → Seguridad y privacidad → Desbloqueo del dispositivo → Desbloqueo facial → introduzca el PIN → complete el registro; después, basta con mirar a la cámara frontal en la pantalla de bloqueo. Para eliminarlo: en Ajustes, modelo facial → Eliminar. Es biometría WEAK, **prohibido** usarla para proteger aplicaciones de pagos o bancarias. La ruta del menú se mantiene como en versiones anteriores y no se ha revisado paso a paso en user-v1.2.

### Identificación de versión

La versión pública es `user-vMAJOR.MINOR`; el número interno `V<número>` está escrito en la imagen. user-v1.2 = V129.

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
