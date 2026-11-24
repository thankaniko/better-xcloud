# BX Community Final — desarrollo suspendido indefinidamente

**Idiomas / Languages / Idiomas / 语言:** [Português (Brasil)](README.md) · [English](README.en.md) · [Español](README.es.md) · [简体中文](README.zh-CN.md)

> [!IMPORTANT]
> **Comunicado oficial del proyecto · 24 de noviembre de 2026.** Versión final experimental 1.0.0. Desarrollo suspendido por tiempo indefinido. No se prevén actualizaciones, parches de seguridad, soporte técnico ni garantías de compatibilidad futura. No es una versión estable.

## 1. Posicionamiento público y motivos

Esta iniciativa independiente nació para mejorar la experiencia de juego en la nube en televisores LG, incluidos equipos sin soporte oficial. Su finalidad fue técnica: hacer medible la transmisión, aprovechar el hardware disponible e investigar la compatibilidad sin acceso root.

Hemos suspendido deliberadamente el desarrollo como protesta pacífica contra los cambios en la política comercial de Xbox Cloud Gaming. En su [anuncio del 3 de septiembre de 2026](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/), Xbox comunicó la introducción de franquicias mensuales de juego en la nube en suscripciones Game Pass anteriormente disponibles sin dichos límites mensuales, junto con la posibilidad de adquirir tiempo adicional. La empresa mencionó los costes operativos, la fiabilidad y la continuidad de las inversiones como motivos. Las condiciones efectivas pueden variar según la cuenta y el mercado.

Nuestra objeción se centra en la reducción de una prestación esencial, especialmente para quienes dependen de la nube. Reconocemos los costes de infraestructura y la necesidad de modelos comerciales sostenibles. Sin embargo, consideramos que restringir una prestación antes ilimitada y cobrar por separado para continuar utilizándola perjudica la previsibilidad, la confianza del consumidor y el valor de la suscripción. Defendemos condiciones transparentes, avisos previos adecuados y un trato proporcional a quienes dependen del servicio.

Esta crítica a una política no constituye una declaración de ilegalidad, una atribución de intenciones no demostradas ni un ataque a empleados, desarrolladores o usuarios. No afirmamos que Microsoft haya copiado a otro proveedor. El proyecto no busca eludir franquicias, pagos o requisitos de suscripción, generar tráfico abusivo ni sabotear el servicio. No promovemos el acoso ni el acceso no autorizado.

El código y el paquete final experimental quedan disponibles con fines de archivo, educación y consulta técnica. Su preservación no implica mantenimiento ni que se hayan alcanzado todos los objetivos. No existe una fecha ni una condición que garantice la reanudación. Esta decisión se limita a esta adaptación independiente y no representa al Better xCloud original ni al proyecto separado webOS Mega Repository.

## 2. Paquete final

[IPK](final/org.webos.community.bxfinal_1.0.0_all.ipk) · [Source ZIP](final/bx-community-final-source.zip)

| Elemento | Estado |
| --- | --- |
| Versión | 1.0.0 — experimental |
| Instalación | Developer Mode de webOS; sin root |
| Red | Sitio oficial de Xbox; sin proxy, NAS ni servidor propio del proyecto |
| Objetivo | TV LG desde 2020; no es una lista de compatibilidad certificada |
| Validación | Estructura, sintaxis JavaScript y pruebas simuladas; streaming final en hardware sin verificar |
| Mantenimiento | Suspendido indefinidamente |

## 3. Comportamiento técnico

El lanzador independiente abre https://play.xbox.com/. El userscript está diseñado para limitarse a los orígenes oficiales de Xbox y excluir las rutas de autenticación. No recopila, exporta ni registra intencionadamente credenciales, cookies, tokens, cabeceras de solicitudes ni URL. No existe un servidor propio de telemetría. Es una descripción de la implementación, no una certificación independiente de seguridad; los servicios de Microsoft conservan sus prácticas habituales de tratamiento de datos.

| Perfil | Comportamiento y límites |
| --- | --- |
| Máximo (predeterminado) | Sin límite local adicional de bitrate o FPS. Prioriza códecs eficientes en Chromium moderno si el navegador los anuncia; permite Auto o AVC. No garantiza la negociación ni la aceleración por hardware. |
| Nativo | Desactiva preferencias de códecs y modificaciones de solicitudes, manteniendo el monitor local. |
| HQ Legacy (experimental) | Adapta la técnica upstream de perfil Tizen solo si la solicitud de sesión existente contiene los campos necesarios. No cambia la versión del navegador, dimensiones o capacidades de códec. Sin redirección externa. Puede degradar o impedir la transmisión; vuelva a Nativo + Auto y reinicie manualmente la sesión. No se garantiza recuperación automática. |

Utilice el selector de Xbox para solicitar la mayor resolución ofrecida. No se fuerzan resoluciones inexistentes, no se anulan límites de bitrate del servidor ni requisitos de acceso. No se garantizan 4K/8K, HDR, AV1, HEVC, 120 FPS ni bitrates arbitrarios; no existe codificador ni escalado propio. Xbox documenta hasta 1440p en situaciones elegibles. El resultado depende del servicio, panel, decodificador y red.

El monitor local muestra resolución RTP/HTML, FPS, bitrate, pérdida de paquetes, jitter, RTT, cuadros descartados, códec, QP medio, tiempo de decodificación y QPS. QP mide cuantización, no controla el codificador remoto. QPS cuenta únicamente las solicitudes fetch observadas al origen de streaming; excluye XHR, otros hosts, workers y tráfico WebRTC. No se aumenta artificialmente. N/D indica medición no disponible, no cero. No se inspeccionan frames ni workers externos. Los bundles Full/Lite anteriores no están incluidos; solo se adapta la técnica aislada de perfil upstream.

## 4. Compatibilidad, instalación y seguridad

El objetivo abarca webOS 5.x (2020), 6.x (2021), 22, 23, 24, 25, 26 y posteriores. La sintaxis conservadora, la detección de API y los mecanismos alternativos no demuestran compatibilidad. El IPK final no se ha validado físicamente en ninguna de estas generaciones. Cambios en navegador, autenticación, sitio o políticas pueden impedir su funcionamiento.

1. Instale mediante Developer Mode y webOS Dev Manager. El ID independiente conserva Probe 0.2.0.
2. Abra el lanzador, seleccione la máxima calidad nativa de Xbox e inicie una sesión.
3. Cambie el perfil o códec desde el panel y reinicie la sesión de juego. F8 en un teclado alterna la visibilidad; reiniciar la aplicación restaura la interfaz. El control permanece vinculado a la página.
4. Si falla, seleccione Nativo + Auto y reinicie, o desinstale y utilice el cliente oficial. No introduzca credenciales si el origen real de inicio de sesión no es un dominio oficial de autenticación de Microsoft; ante dudas, deténgase.

No se prevén actualizaciones, incluso ante problemas de seguridad o compatibilidad. Se recomienda el cliente oficial para el uso habitual. Las pruebas estáticas y simuladas no sustituyen la validación empírica ni una revisión de seguridad. El software se entrega tal cual, bajo las condiciones de la licencia MIT.

## 5. Reproducción e integridad

Extraiga el ZIP de código fuente y ejecute desde su raíz (requiere Python 3, `ar` y Node.js):

```sh
python3 build.py
node --check app/probe.js
node --check app/webOSUserScripts/userScript.js
node tests/mock.js
```

Se validaron la estructura del paquete, la sintaxis JavaScript y las pruebas simuladas de alcance, códecs y alternativas. No acreditan funcionamiento en hardware real. Compruebe los SHA-256 de los archivos distribuidos sin modificaciones:

| File | SHA-256 |
| --- | --- |
| `org.webos.community.bxfinal_1.0.0_all.ipk` | `414a24412dba77639932691c3b6f616657b912bccd612cc4b9f73c46002aac36` |
| `bx-community-final-source.zip` | `3aa1412ab473e4dc6e6308f7e57ec86ecd3963515797003e2699024777a0c2ab` |

Los archivos de [final/](final/) son artefactos de archivo, no una GitHub Release estable ni un paquete del catálogo principal de webOS Mega Repository. Esta revisión documental no modifica el binario ni el ZIP archivados.

## 6. Referencias y atribución

Proyecto independiente y no oficial, sin afiliación a Microsoft, Xbox, LG ni mantenedores originales. Basado en Better xCloud de redphx bajo MIT; se conservan los avisos y créditos originales. Las marcas pertenecen a sus titulares. El README upstream se conserva por separado para evitar confundir sus instrucciones de soporte y donaciones con esta adaptación suspendida.

- [Xbox Wire — cloud gaming policy announcement (2026-09-03)](https://news.xbox.com/en-us/2026/09/03/xbox-cloud-gaming-changes/)
- [Xbox Wire — 1440p streaming](https://news.xbox.com/pt-br/2026/02/25/atualizacao-de-fevereiro-do-xbox-streaming-em-1440p-nos-consoles-xbox-atualizacoes-do-rog-xbox-ally-e-mais/)
- [Better xCloud](https://github.com/redphx/better-xcloud) · [Features](https://better-xcloud.github.io/features/) · [FAQ](https://better-xcloud.github.io/faq/)
- [LG webOS — Web API and web engine](https://webostv.developer.lge.com/develop/specifications/web-api-and-web-engine)
- [webOS Brew — userscripts](https://www.webosbrew.org/pages/web-development/#userscripts-in-apps)
- [W3C — WebRTC](https://www.w3.org/TR/webrtc/)
- [MIT LICENSE](LICENSE) · [Original upstream README](docs/UPSTREAM-README.md)

**Estado final: desarrollo suspendido indefinidamente.** Sin compromiso de reanudación, reparación ni actualización.
