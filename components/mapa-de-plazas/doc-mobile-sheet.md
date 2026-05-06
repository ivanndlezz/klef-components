# Documentación CSS: Bottom Sheet (Mobile) - Mapa de Plazas

Este documento detalla las especificaciones técnicas y visuales del componente `lbcs-sheet` cuando se visualiza en dispositivos móviles (pantallas ≤ 600px).

## 1. Contenedor Principal (`#lbcs-sheet`)

El contenedor se transforma en una "hoja inferior" (Bottom Sheet) que emerge desde la parte baja de la pantalla.

- **Posicionamiento**: `fixed` en la parte inferior (`bottom: 0`, `left: 0`, `right: 0`).
- **Dimensiones**:
  - Ancho: `100%` (ocupa todo el ancho del viewport).
  - Altura Máxima: `80vh` (permite ver parte del mapa al fondo).
- **Estética**:
  - Fondo: `var(--white)` (#ffffff).
  - Bordes Superiores: Redondeados con `var(--radius-lg)` (20px).
  - Borde Superior: `1px solid var(--border)` (0, 150, 136, 0.15).
- **Animación**:
  - Estado Cerrado: `transform: translateY(100%)`.
  - Estado Abierto: `transform: translateY(0)`.
  - Transición: `transform 0.3s cubic-bezier(0.4, 0, 0.2, 1)`.

## 2. Elementos de Interacción Superior

### Tirador Visual (`.sheet-handle`)
Visible solo en modo mobile para indicar que el elemento se puede deslizar o cerrar.
- **Dimensiones**: 40px x 4px.
- **Color**: `var(--border)` (Verde teal muy suave).
- **Márgenes**: `12px` superior y centrado horizontalmente (`auto`).

### Cabecera (`.sheet-head`)
- **Padding**: `16px 18px 14px`.
- **Estructura**: Flexbox (`display: flex`, `align-items: center`, `gap: 12px`).
- **Logo Circular**: 50px x 50px, borde verde suave, imagen centrada al 80%.
- **Título**: Fuente **Syne**, 16px, peso 700 (Bold), color `var(--ink)` (#0d1f1e).
- **Botón Cerrar**: 30px x 30px, borde redondeado de 8px, icono "✕".

## 3. Cuerpo de la Información (`.sheet-body`)

### Imagen Principal (`.sheet-logo-big`)
- **Altura**: 110px.
- **Fondo**: Imagen de la plaza con `background-size: contain`.
- **Bordes**: Redondeados (12px) y borde sutil.

### Grilla de Datos (`.info-grid` / `.info-row`)
- **Alineación**: Flexbox con `justify-content: space-between`.
- **Responsive Handling**: 
  - `align-items: flex-start` (para que las etiquetas no se desplacen si el valor es largo).
  - `word-break: break-word` en los valores.
- **Tipografía**: 13px. Etiqueta en color suave (`--ink-soft`), valor en color fuerte (`--ink`).

## 4. Acciones Inferiores (`.sheet-actions`)

Las acciones se apilan verticalmente para facilitar el uso con el pulgar.

- **Layout**: `display: flex`, `flex-direction: column`, `gap: 8px`.
- **Botón Principal ("Abrir en Google Maps")**:
  - Color: `var(--teal)` (#009688).
  - Texto: Blanco.
  - Padding: 11px.
- **Botón Secundario ("Ver en mapa")**:
  - Estilo: Outlined (`border: 1px solid var(--teal)`).
  - Color de texto: `var(--teal)`.

## 5. Capa de Fondo (`#lbcs-overlay`)

- **Efecto**: `backdrop-filter: blur(2px)`.
- **Color**: Fondo oscuro semitransparente (`rgba(10, 28, 27, 0.4)`).
- **Comportamiento**: Al hacer clic en esta zona, se dispara `LBCS.closeSheet()`.
