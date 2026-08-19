# BONA Electricidad — Landing page

Landing de una sola pantalla para BONA (Gonzalo Bonavena, electricista matriculado
COPIME N3, zona norte GBA). Un solo archivo `index.html`, sin build step, pensada
para GitHub Pages.

## Contenido pendiente de completar

- **Fotos reales**: reemplazar los 6 `<div class="foto-ph">` de la sección
  "Trabajos realizados" por `<img>` reales con `alt` descriptivo, ej.:
  ```html
  <img src="fotos/tablero-martinez.jpg" alt="Instalación de tablero eléctrico en Martínez">
  ```
  Mantené `object-fit: cover` (ya está en `.galeria img`).
- **og-image.png**: hoy es un placeholder generado (blueprint con el texto "BONA").
  Cuando haya fotos reales de trabajos, conviene reemplazarlo por una imagen real
  de 1200×630px para que se vea mejor al compartir en WhatsApp/Instagram.

## Deploy a GitHub Pages

1. Crear un repo vacío en GitHub: `guardvalker/bona-landing` (público).
2. Pushear este directorio:
   ```bash
   git push -u origin main
   ```
3. En GitHub → Settings → Pages → Source: "Deploy from a branch" → branch `main`,
   carpeta `/ (root)`.
4. Confirmar que carga en `https://guardvalker.github.io/bona-landing/`.

## Apuntar el dominio propio (bonaelectricidad.com.ar)

Cuando el dominio esté listo:

1. Crear un archivo `CNAME` en la raíz del repo con una sola línea:
   ```
   bonaelectricidad.com.ar
   ```
   (GitHub Pages también deja hacer esto desde Settings → Pages → Custom domain,
   que crea el archivo automáticamente).
2. En el proveedor del dominio (donde se compró bonaelectricidad.com.ar), configurar
   los registros DNS. Esto es lo que suele confundirse — son dos cosas distintas:
   - El archivo `CNAME` del repo le dice a GitHub Pages qué dominio servir.
   - Los registros DNS le dicen a internet dónde está ese dominio.

   Para un dominio **apex** (sin `www`, como `bonaelectricidad.com.ar`), GitHub
   Pages requiere registros **A** (no CNAME) apuntando a estas 4 IPs:
   ```
   185.199.108.153
   185.199.109.153
   185.199.110.153
   185.199.111.153
   ```
   Si además se quiere que `www.bonaelectricidad.com.ar` funcione, agregar un
   registro **CNAME** para `www` apuntando a `guardvalker.github.io`.
3. Esperar la propagación DNS (puede tardar de minutos a algunas horas) y
   verificar en Settings → Pages que GitHub confirma el dominio (checkbox
   "Enforce HTTPS" debería quedar disponible una vez verificado).
4. Actualizar `og:image` en `index.html` si se quiere que apunte al dominio
   propio en vez de `guardvalker.github.io` (no es obligatorio, ambas URLs sirven
   la misma imagen mientras el repo esté en Pages).

## Actualizar el número de WhatsApp o Instagram

Ambos están hardcodeados en `index.html` en dos lugares cada uno (CTA del pitch
y footer):
- WhatsApp: buscar `wa.me/5491130147081` — es el número completo con código de
  país (54), sin el `9` mostrado en pantalla, formato requerido por el link de
  WhatsApp. El texto visible en el footer (`+11 3014 7081`) es intencionalmente
  distinto — formato local, sin código de país, para no confundir a la audiencia
  de zona norte.
- Instagram: buscar `gonzalo.bonavena`.
