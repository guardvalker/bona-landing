# BONA Electricidad — Landing page

**App:** https://bonaelectricidad.com.ar

Landing de una sola pantalla para BONA (Gonzalo Bonavena, electricista matriculado
COPIME N3, zona norte GBA): presentación, galería de trabajos y contacto por
WhatsApp/Instagram. Un solo archivo `index.html`, sin build step, pensada
para GitHub Pages.

## Contenido pendiente de completar

- **Más fotos**: la galería tiene 3 fotos reales (`fotos/`), recortadas de las
  fotos originales de Mercado Libre para sacar la franja de marca del pie
  (esas ya la tienen incorporada, pensada para el flyer, no para esta grilla).
  El spec permite hasta 6 — para agregar una nueva:
  ```html
  <img src="fotos/nombre-descriptivo.jpg" alt="Descripción real de la foto">
  ```
  Conviene optimizar cada foto antes de subirla (mismo criterio que las
  actuales: recorte a ~900px de ancho, JPEG calidad ~80) para no pesar la
  carga inicial.
- **og-image.png**: hoy es un placeholder generado (blueprint con el texto "BONA").
  Se puede reemplazar por una de las fotos reales de trabajo (1200×630px) para
  que se vea mejor al compartir en WhatsApp/Instagram.

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
