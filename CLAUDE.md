# FYPRO Inventory

App web de control de inventario para FYPRO. Sin frameworks — HTML, CSS y JS vanilla en un solo archivo.

## Levantar el proyecto

```bash
cd "C:\Users\USUARIO\Desktop\test claude"
python -m http.server 3000
```

URL: http://localhost:3000/inventory.html

## Archivos

| Archivo | Descripción |
|---|---|
| `inventory.html` | **App principal** — todo el código en un solo archivo (HTML + CSS + JS) |
| `index.html` | Proyecto tocadiscos (no relacionado, ignorar) |
| `style.css` | Estilos del tocadiscos (no relacionado, ignorar) |

## Repositorio

https://github.com/cokealvarezd/fypro-inventory

Subir cambios después de cada feature o fix significativo.

## Persistencia de datos

Los datos se guardan en **localStorage del navegador**:

| Clave | Contenido |
|---|---|
| `inv_productos` | Catálogo de productos |
| `inv_movimientos` | Historial de todos los movimientos |

La app tiene botones de **exportar/importar JSON** para respaldo y migración entre equipos.

## Estructura del estado (JS)

```js
state.productos   // Array de productos
state.movimientos // Array de movimientos

// Producto
{
  id,            // generado con generarId('prod')
  marca,
  nombre,
  categoria,
  precioCosto,       // neto
  precioCostoIVA,
  precioVenta,       // neto
  precioVentaIVA,
  activo             // boolean (soft delete)
}

// Movimiento
{
  id,            // generado con generarId('mov')
  tipo,          // 'COMPRA' | 'VENTA'
  ubicacion,     // 'PRINCIPAL' | 'TINYSHOP'
  fecha,         // 'YYYY-MM-DD'
  comentario,
  items: [{ productoId, cantidad }]
}
```

## Tiendas

- **PRINCIPAL** — Tienda principal
- **TINYSHOP** — Tienda TinyShop

## Tipos de movimiento

- **COMPRA** → aumenta stock
- **VENTA** → disminuye stock

## Convenciones de código

- **Idioma UI:** español en todo texto visible
- **Moneda:** CLP (pesos chilenos), sin decimales — usar siempre `formatearMoneda(n)`
- **Fechas:** almacenar como `'YYYY-MM-DD'`, mostrar con `formatearFecha(iso)` → `DD/MM/YYYY`
- **IDs:** generar con `generarId('prefijo')`
- **HTML dinámico:** escapar siempre con `escapeHtml()` antes de insertar en innerHTML
- **Guardar cambios:** llamar `guardarDatos()` después de toda mutación al estado
- **Re-render:** llamar `renderVista(state.vistaActual)` para refrescar la vista activa

## Marcas actuales

Garmin, Cleverace, Precision Fuel, Strive, Underfive, Sockslab

## Categorías actuales

GPS Cartográficos e-Trex, GPS Cartográficos GPS Map, GPS Línea Montana, Equipos para Automovil/Moto, GPS Marino, Radios Garmin, Chartplotter/Ecosondas, Ecosondas con GPS, Accesorios Chartplotter/Ecosondas, Radares y AIS, Equipos GPS con mensajería inReach, Relojes y Ciclocomputadores, Accesorios Relojes y Ciclocomputadores, Alimentación Deportiva, Ropa deportiva, Otros

## Qué NO hacer

- No agregar frameworks (React, Vue, etc.) — el proyecto es vanilla a propósito
- No dividir en múltiples archivos JS/CSS — todo vive en `inventory.html`
- No poner decimales en precios CLP
- No modificar `index.html` ni `style.css` (son del proyecto tocadiscos)
