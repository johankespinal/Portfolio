# WP Fleet Manager — WordPress por lotes (MVP 0.1)

**Herramienta pública y gratuita para inspeccionar numerosas instalaciones WordPress** desde una cuenta de hosting con SSH o Terminal de cPanel.

Analiza sin modificar los sitios. Busca instalaciones de WordPress y, si hay WP-CLI disponible, consulta la versión del core y el número de actualizaciones pendientes de plugins y temas. Genera informes en **CSV y HTML**.

> Estado: prototipo funcional a nivel de código. Se verificó su sintaxis y ayuda de consola, pero **no se ha probado contra un servidor real con múltiples WordPress**. Se recomienda probarlo primero en un entorno de pruebas.

## Requisitos

- Python 3.8+ (biblioteca estándar; no requiere instalar paquetes).
- Terminal o acceso SSH en tu hosting.
- Opcional: WP-CLI disponible como `wp`.
- Ejecútalo como **usuario normal de la cuenta**, nunca como root.

## Uso rápido

Desde la carpeta donde descargaste el script:

```bash
# Primer ensayo: solo detectar instalaciones, sin invocar WordPress
python3 wp_fleet.py --root "$HOME/public_html" --no-wpcli

# Auditoría con WP-CLI si está instalado
python3 wp_fleet.py --root "$HOME" --depth 5 --output "$HOME/wp-fleet-report"
```

Opciones disponibles: `--root`, `--depth`, `--max-sites`, `--timeout`, `--no-wpcli`, `--output`. Ejecuta `python3 wp_fleet.py --help` para consultar la ayuda.

El comando crea `wp-fleet-report.csv` y `wp-fleet-report.html` en el destino indicado. Para no exponer las rutas internas, guarda los informes **fuera de `public_html`** y no publiques los reportes en GitHub.

## Alcance y seguridad

- No elimina archivos, no actualiza plugins, no cambia bases de datos ni contraseñas.
- Comprueba que `wp-config.php`, `wp-admin` y `wp-includes` existen, sin abrir ni copiar el archivo de credenciales.
- No sigue enlaces simbólicos ni escanea carpetas comunes de respaldos.
- El modo WP-CLI invoca comandos de consulta con `--skip-plugins --skip-themes`; algunos `mu-plugins` y código de arranque pueden seguir ejecutándose. **En instalaciones sospechosas, utiliza primero `--no-wpcli`.**
- No verifica malware, seguridad integral ni la compatibilidad de actualizaciones; su función es ofrecer un inventario técnico inicial.
- Para varias cuentas cPanel diferentes, ejecutar por cuenta autorizada y consolidar informes posteriormente.

## Próximos pasos

Verificación de integridad de WordPress, control de espacio, auditoría por plugin y comparación de auditorías anteriores.

**Autor:** Johan K. Espinal · [Portafolio](../../README.md)
