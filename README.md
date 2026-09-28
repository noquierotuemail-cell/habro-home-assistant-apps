# HABRO Local Beta para Home Assistant

Prueba privada de acceso a HABRO desde la red local o VPN, sin Nabu Casa y sin publicar Home Assistant en Internet.

## Instalar

1. En Home Assistant, abre **Ajustes → Aplicaciones → Tienda → Repositorios** (en algunas versiones, **Complementos → Tienda**).
2. Añade `https://github.com/noquierotuemail-cell/habro-home-assistant-apps#beta-local-access`.
3. Instala **HABRO Local Beta**, inicia la aplicación y pulsa **Abrir interfaz web**.
4. Accede a Home Assistant por su dirección local o la de tu VPN, en el mismo navegador. En la conexión de HABRO, introduce la URL base de Home Assistant, por ejemplo `http://homeassistant.local:8123` o `http://192.168.1.10:8123`, y autoriza el acceso.

Esta rama es una beta separada. **HABRO Installer** mantiene su arranque manual y su configuración existente. La aplicación local se abre dentro de Home Assistant mediante Ingress. La URL que use el navegador debe llegar a Home Assistant durante toda la prueba; por VPN utiliza la dirección accesible a través de ella. No hace falta abrir puertos en el router.

Si aparece un error, anota el paso, la URL base introducida, el navegador y el mensaje exacto; oculta tokens y datos personales antes de compartir capturas o registros.
