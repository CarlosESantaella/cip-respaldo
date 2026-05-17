# CIP — Respaldo del sitio (cip.org.uy)

Repositorio de respaldo y referencia del sitio WordPress **cip.org.uy** (Colegio de Ingenieros del Perú / landing institucional).

> Este repositorio sirve como punto de control y documentación del proyecto. El respaldo binario completo del sitio (archivos + base de datos) se mantiene en Google Drive por razones de tamaño y seguridad.

---

## Stack

| Componente | Detalle |
|---|---|
| CMS | WordPress |
| Tema | Astra |
| Constructor | Elementor + Ultimate Addons for Gutenberg (Spectra) |
| Formularios | Contact Form 7 / SureForms |
| SEO | SureRank |
| Caché | LiteSpeed Cache |
| Correo | WP Mail SMTP |
| Chat | WP Live Chat Support |
| Hosting producción | Hostinger |
| Entorno local | Laragon (Apache + MySQL 8) |

## Estructura del proyecto

```
cip-wordpress/
├── wp-admin/           # Núcleo de WordPress (no modificar)
├── wp-includes/        # Núcleo de WordPress (no modificar)
├── wp-content/
│   ├── themes/         # Astra y temas por defecto
│   ├── plugins/        # Plugins activos
│   ├── uploads/        # Media del sitio (~84 MB)
│   └── languages/
├── wp-config.php       # Configuración (NO versionar — contiene credenciales)
└── README.md
```

## Entorno local (Laragon)

1. Clonar este repositorio dentro de `C:\laragon\www\`.
2. Restaurar el respaldo completo desde Google Drive (ver sección **Respaldo** abajo) sobre el mismo directorio.
3. Crear una base de datos local llamada `cip_wordpress` en MySQL.
4. Importar el dump SQL incluido en el respaldo.
5. Editar `wp-config.php` con las credenciales locales (Laragon por defecto: `root` sin contraseña).
6. Acceder a `http://cip-wordpress.test`.

> Si las URLs internas apuntan al dominio de producción, ejecutar un *search & replace* sobre la BD para reemplazar `https://cip.org.uy` por `http://cip-wordpress.test`.

## Respaldo del sitio

El respaldo completo (archivos + base de datos) se guarda en **Google Drive** como archivo comprimido. Contiene:

- Volcado SQL de la base `cip_wordpress` (mysqldump)
- Carpeta `wp-content/` completa (temas, plugins y uploads)
- Archivos raíz de WordPress

### Cómo restaurar

1. Descargar el archivo `cip-wordpress-backup-YYYY-MM-DD.zip` desde Google Drive.
2. Descomprimir sobre un WordPress limpio o sobre `C:\laragon\www\cip-wordpress\`.
3. Importar el `.sql` incluido a la base de datos.
4. Ajustar `wp-config.php` según el entorno destino.

### Cómo regenerar el respaldo

Desde la raíz del proyecto, ejecutar el script de respaldo (o seguir los pasos del comando `mysqldump` + zip).

## Seguridad

- **No commitear `wp-config.php`** — contiene credenciales de la BD de producción.
- **No commitear archivos `.sql`** crudos ni respaldos `.wpress`/`.zip`.
- Estos archivos están listados en `.gitignore`.

## Convenciones

- Toda personalización del tema debe ir en un **child theme de Astra**, nunca tocar el tema padre directamente.
- Plugins se actualizan primero en local, se validan, y recién después en producción.
- Mantener uniformidad de estilos con la guía visual de Elementor del sitio.

## Contacto

- Sitio: https://cip.org.uy
- Admin del proyecto: javier.at88@gmail.com
