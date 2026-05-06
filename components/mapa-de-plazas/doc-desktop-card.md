# Documentación: Nuevo Comportamiento Desktop (Floating Card)

Este documento detalla los cambios técnicos realizados en el componente `mapa-de-plazas` para implementar la nueva interfaz de tarjeta flotante en versiones de escritorio.

## 1. Estructura HTML (Refactorización)

Para permitir que la tarjeta de información se posicione relativa al mapa y no a toda la ventana del navegador, se introdujo un nuevo contenedor de área:

- **Contenedor `#lbcs-map-area`**: Se envolvió el div del mapa (`#lbcs-map`) y los elementos de la hoja de información (`#lbcs-sheet` y `#lbcs-overlay`) en este nuevo contenedor con `position: relative`.
- **Relocalización**: El HTML de la hoja (`#lbcs-sheet`) se movió desde el final del body hacia el interior de `#lbcs-map-area`.

```html
<div id="lbcs-wrap">
  <div id="lbcs-map-area" style="position: relative; overflow: hidden">
    <div id="lbcs-map"></div>
    <div id="lbcs-overlay" onclick="LBCS.closeSheet()"></div>
    <div id="lbcs-sheet">...</div>
  </div>
</div>
```

## 2. Cambios en CSS (Media Queries)

El cambio más significativo ocurre en el breakpoint `min-width: 601px`.

### Posicionamiento y Layout

- **De Side-Sheet a Floating Card**: Se cambió `fixed` por `absolute` para que la tarjeta flote dentro del mapa.
- **Coordenadas**: Se posicionó en `bottom: 24px` y `right: 24px`.
- **Dimensiones**: Se aumentó el ancho a `380px` para una mejor jerarquía visual en pantallas grandes.

### Estética y UX

- **Sombra y Bordes**: Se aplicó una sombra más profunda (`box-shadow: 0 15px 45px rgba(0,0,0,0.15)`) y se redondearon todas las esquinas (`border-radius: var(--radius-lg)`).
- **Animación**: Se reemplazó el deslizamiento lateral (`translateX`) por una transición suave de opacidad y desplazamiento vertical (`translateY`).
- **Overlay**: Se ocultó el `#lbcs-overlay` en desktop (`display: none !important`) para permitir que el usuario siga navegando por el mapa mientras la tarjeta está abierta.

### Tipografía y Espaciado

- **Padding**: Se incrementó el padding del cuerpo a `24px` y el del encabezado a `20px 24px 16px`.
- **Textos**: Se subió el tamaño de fuente de los títulos a `18px` y de las filas de información a `14px`.
- **Botones**: Se aumentó el padding vertical a `14px` para darles más presencia y evitar que luzcan "flacos".

## 3. Cambios en JavaScript (Lógica de Interacción)

Aunque la lógica central de Leaflet no cambió, se ajustó la hidratación de la lista para mejorar la experiencia de usuario.

### Función `skell()` (Template)

Se modificó el manejador de eventos del botón "Ver en mapa" para que ejecute dos acciones secuenciales:

1.  **`zoomTo(id)`**: Centra el mapa en las coordenadas de la plaza.
2.  **`openSheet(id)`**: Dispara la apertura de la tarjeta de información.

```javascript
// Antes:
<button onclick="LBCS.zoomTo('{id}')">Ver en mapa</button>

// Después:
<button onclick="LBCS.zoomTo('{id}'); LBCS.openSheet('{id}')">Ver en mapa</button>
```

### Clase `.open`

La lógica de JavaScript sigue simplemente añadiendo o quitando la clase `.open`. Gracias al cambio en CSS, esta misma clase ahora dispara la animación de "aparición" (fade-in + slide-up) en lugar del "deslizamiento" lateral previo.

---

Estos cambios aseguran que el componente se sienta como una aplicación moderna y pulida, optimizando el espacio en pantallas grandes sin sacrificar la funcionalidad en dispositivos móviles.
