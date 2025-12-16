# Buscador público por número (sin autenticación)

Este proyecto es un sitio estático que carga un **JSON público** (`data.json`) y permite buscar por número para mostrar información.

## Estructura
```
/index.html
/data.json
```

## Publicación rápida

### Opción 1: GitHub Pages
1. Crea un repositorio y sube estos archivos.
2. En **Settings → Pages**, selecciona **Source: `main`** y **`/root`**.
3. Abre la URL pública que te da GitHub Pages.

### Opción 2: Netlify
1. Entra a https://app.netlify.com y arrastra la carpeta.
2. Netlify desplegará la web y te dará una URL pública.

## Actualizar datos desde SharePoint
SharePoint no expone datos sin autenticación. Para publicar datos **sin autenticación**, exporta y publica un JSON:

1. **Exportar desde SharePoint a Excel/CSV**:
   - Abre la lista → **Export to Excel** (obtendrás un archivo `.xlsx`).
   - Convierte a **CSV** si prefieres.
2. **Transformar a JSON**:
   - Utiliza Excel, Power Query o scripts para producir `data.json` con las columnas necesarias.
3. **Sube el `data.json` al mismo sitio** (GitHub/Netlify).
4. **(Opcional) Automatiza con Power Automate**: Crea un flujo que periódicamente exporte la lista y actualice el `data.json` en tu repositorio o en un almacenamiento público.

## Cambiar la fuente de datos
En `index.html` busca la constante `DATA_URL`. Si alojas el `data.json` en otro dominio, reemplázala por esa URL completa.

## Búsqueda parcial (opcional)
Para permitir coincidencias por prefijo o contiene, reemplaza:
```js
const registro = tabla.find(r => String(r.numero).trim() === n);
```
por
```js
const resultados = tabla.filter(r => String(r.numero).includes(n));
// y muestra una tabla con múltiples filas
```

## Notas
- Publica solo datos **no sensibles**.
- Si usas otro dominio para el JSON, asegúrate que permita **CORS**.
- Desactiva el caché con `cache: 'no-store'` (ya está en el código) o añade un query param `?v=timestamp` cuando actualices.
