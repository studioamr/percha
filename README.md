# PERCHA

Tienda de ropa seminueva y nueva de Coco. Catálogo público + panel de administración, sin servidor.

- **Catálogo:** https://studioamr.github.io/percha/
- **Panel (Coco):** https://studioamr.github.io/percha/admin.html

## Cómo funciona

- El inventario vive en el teléfono de Coco (IndexedDB del navegador, fotos incluidas).
- «Publicar» sube `catalogo.json` + las fotos nuevas a este repo con la API de GitHub (un commit por publicación). GitHub Pages sirve el catálogo.
- Los pedidos llegan por WhatsApp con `wa.me` — sin API de Meta.
- Las prendas vendidas se quedan en el panel (para stats de ingreso) pero se excluyen del catálogo al publicar.

## Puesta en marcha (una sola vez, en el teléfono de Coco)

1. Abrir el panel y guardarlo en pantalla de inicio.
2. **Ajustes → WhatsApp de pedidos:** su número con lada 52 (ej. `524430000000`).
3. **Código de conexión (token):** André lo genera y se lo manda como *link mágico*:
   - https://github.com/settings/personal-access-tokens/new
   - Token name: `percha-coco` · Expiration: 1 año (custom)
   - Resource owner: **studioamr** · Only select repositories → **percha**
   - Repository permissions → **Contents: Read and write**. Nada más.
   - Generar, copiar el token y mandarle a Coco el link:
     `https://studioamr.github.io/percha/admin.html#token=EL_TOKEN`
   - Al abrirlo, el panel guarda el token solo y limpia la URL. «Probar conexión» debe dar ✓.
4. Dar de alta una prenda de prueba y **Publicar**.

## Notas técnicas

- El panel siempre debe abrirse en el **mismo navegador** del teléfono (ahí viven los datos). «Respaldo» descarga todo (con fotos) por si cambia de teléfono; «Importar del catálogo publicado» reconstruye el inventario desde lo ya publicado.
- Fotos comprimidas en el cliente a máx. 1000 px JPEG (~80 KB c/u). 500 prendas ≈ 40 MB en el repo, sin problema.
- Dev local: `python3 -m http.server 4340` en esta carpeta.
