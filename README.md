# CSS Avanzado

### 1. :has() - El Parent Selector

El selector `:has()` es una de las características más esperadas en CSS, ya que permite seleccionar elementos basados en sus elementos hijos o descendientes. Este selector es comúnmente conocido como "parent selector" (selector de padre).

#### Sintaxis básica
```css
/* Selecciona párrafos que contienen enlaces */
p:has(a) { /* estilos */ }

/* Selecciona elementos que contienen una imagen seguida de un párrafo */
div:has(img + p) { /* estilos */ }
```

#### Casos de uso prácticos
- Estilizar formularios basados en el estado de sus inputs
- Modificar tarjetas que contienen ciertos elementos
- Adaptar layouts según el contenido interno

### 2. :is(), :where() y :not() - Simplificando Selectores

Estos selectores funcionales ayudan a escribir CSS más limpio y mantenible, reduciendo la repetición de código.

#### :is()
Permite agrupar selectores de manera más concisa:
```css
/* En lugar de escribir */
header p, main p, footer p { color: blue; }

/* Podemos escribir */
:is(header, main, footer) p { color: blue; }
```

#### :where()
Similar a `:is()`, pero con especificidad cero:
```css
/* Útil para crear estilos base fácilmente sobrescribibles */
:where(article, section) p { color: #333; }
```

#### :not()
Permite seleccionar elementos que no coinciden con ciertos criterios:
```css
/* Selecciona todos los párrafos que no son la primera línea */
p:not(:first-of-type) { margin-top: 1em; }
```

### 3. :nth-child(n of selector) - Selección Precisa

Esta nueva sintaxis del selector `:nth-child()` permite una selección más específica de elementos.

#### Sintaxis y ejemplos
```css
/* Selecciona el segundo párrafo entre los elementos p */
p:nth-child(2 of p) { font-weight: bold; }

/* Selecciona elementos pares solo entre las imágenes */
img:nth-child(even of img) { border: 2px solid blue; }
```

#### Ventajas
- Mayor precisión en la selección de elementos
- Reduce la necesidad de clases adicionales
- Mejora la mantenibilidad del código

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---

### 4. Container Queries - Diseño Adaptable por Contenedor

Los Container Queries representan una evolución en el diseño responsive, permitiendo que los elementos se adapten basándose en el tamaño de su contenedor en lugar del viewport.

#### Diferencias con Media Queries
```css
/* Media Query tradicional - basado en viewport */
@media (min-width: 768px) {
  .card { flex-direction: row; }
}

/* Container Query - basado en contenedor */
@container (min-width: 400px) {
  .card { flex-direction: row; }
}
```

#### Implementación Básica
```css
/* Definir el contenedor */
.container {
  container-type: inline-size;
  container-name: main-container;
}

/* Estilos basados en el contenedor */
@container main-container (min-width: 600px) {
  .component {
    display: grid;
    grid-template-columns: 1fr 2fr;
  }
}
```

#### Casos de uso prácticos
- Componentes de tarjetas adaptables
- Layouts de galería flexibles
- Navegación responsive basada en espacio disponible
- Widgets que se adaptan a diferentes áreas de contenido

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---

Este módulo explora características avanzadas de CSS que permiten crear diseños más flexibles y mantenibles. Estas herramientas modernas proporcionan mayor control sobre la presentación y el comportamiento de los elementos en diferentes contextos.

### 4. Funciones Modernas de Color y Accesibilidad

CSS ha evolucionado para ofrecer nuevas funciones de manipulación de color y espacios de color más precisos, mejorando tanto la creatividad como la accesibilidad.

#### color-mix() - Mezclando Colores
```css
/* Mezcla básica de colores */
.elemento {
  /* Mezcla 50-50 de azul y rojo */
  background-color: color-mix(in srgb, blue 50%, red);
  
  /* Mezcla con transparencia */
  border-color: color-mix(in srgb, #00000080 50%, #ffffff);
}
```

#### color-contrast() - Contraste Automático
```css
/* Selecciona automáticamente el color con mejor contraste */
.texto-adaptativo {
  color: color-contrast(var(--background-color) vs
    black, white, #777777);
}
```

#### Nuevos Espacios de Color

##### OKLCH y OKLAB
```css
.elemento-moderno {
  /* OKLCH: Luminancia, Croma, Matiz */
  color: oklch(70% 0.15 180);
  
  /* OKLAB: Más preciso perceptualmente */
  background-color: oklab(70% -0.05 0.1);
}
```

##### HWB (Hue, Whiteness, Blackness)
```css
.elemento-hwb {
  /* HWB: Más intuitivo para diseñadores */
  color: hwb(200 30% 10%);
  background-color: hwb(0 100% 0%); /* Blanco puro */
}
```

#### Mejores Prácticas de Accesibilidad

- Usar `color-contrast()` para garantizar legibilidad
- Implementar temas claros y oscuros con nuevos espacios de color
- Verificar ratios de contraste con herramientas modernas
- Considerar daltonismo al elegir combinaciones de colores

#### Ventajas de los Nuevos Espacios de Color
- Mayor precisión en la representación de colores
- Mejor manejo de la gama de colores en diferentes dispositivos
- Transiciones más suaves y naturales
- Mayor control sobre la percepción del color

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---

### 5. CSS Variables y Custom Properties - Mejoras Avanzadas

Las variables CSS y propiedades personalizadas han evolucionado para ofrecer mayor funcionalidad y tipado, permitiendo crear sistemas de diseño más robustos y dinámicos.

#### Variables CSS con @property
```css
/* Definición de una variable CSS tipada */
@property --main-color {
  syntax: '<color>';
  initial-value: #1a1a1a;
  inherits: true;
}

/* Uso de la variable tipada */
.element {
  background-color: var(--main-color);
  transition: --main-color 0.3s ease;
}
```

#### Funciones CSS Avanzadas

##### calc(), min(), max() y clamp()
```css
/* Cálculos dinámicos */
.container {
  /* Calcula el ancho basado en el viewport */
  width: calc(100vw - 2rem);
  
  /* Establece límites mínimos y máximos */
  font-size: clamp(1rem, 2vw, 2rem);
  
  /* Usa min() y max() para valores responsivos */
  padding: min(5vw, 50px);
  margin: max(20px, 2vh);
}
```

#### Casos de uso prácticos

##### Sistema de Temas Dinámicos
```css
:root {
  --primary-hue: 220;
  --theme-primary: hsl(var(--primary-hue) 70% 50%);
  --theme-secondary: hsl(calc(var(--primary-hue) + 180) 70% 50%);
}

/* Tema oscuro */
[data-theme="dark"] {
  --primary-hue: 240;
  --theme-background: hsl(var(--primary-hue) 15% 15%);
  --theme-text: hsl(var(--primary-hue) 15% 85%);
}
```

##### Animaciones con Variables CSS
```css
.animated-element {
  --x-position: 0;
  transform: translateX(var(--x-position));
  transition: --x-position 0.3s ease;
}

.animated-element:hover {
  --x-position: 100px;
}
```

#### Ventajas y Mejores Prácticas
- Tipado fuerte con @property para mejor control y validación
- Transiciones y animaciones más eficientes
- Sistemas de diseño escalables y mantenibles
- Temas dinámicos con cambios en tiempo real
- Mejor rendimiento que las variables de JavaScript

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---

### 6. Optimización de Rendimiento en CSS

La optimización del rendimiento en CSS es crucial para crear sitios web rápidos y eficientes. Las nuevas características y técnicas nos permiten mejorar significativamente el rendimiento sin comprometer la experiencia del usuario.

#### content-visibility y contain
```css
/* Optimiza el renderizado de secciones fuera de la vista */
.seccion-larga {
  content-visibility: auto;
  contain-intrinsic-size: 0 500px;
}

/* Aísla el contenido para mejor rendimiento */
.componente-complejo {
  contain: content;
  contain: strict;
}
```

#### Carga Progresiva de Estilos
```css
/* Estilos críticos inline */
.header {
  /* Estilos mínimos para el primer render */
  display: flex;
  padding: 1rem;
}

/* Estilos no críticos en archivo separado */
@import url('estilos-no-criticos.css') layer(enhancement);

/* Carga condicional de estilos */
@layer enhancement {
  @media (min-width: 768px) {
    .header {
      /* Estilos adicionales para desktop */
      backdrop-filter: blur(10px);
    }
  }
}
```

#### Minimización de Reflows y Repaints
```css
/* Uso de propiedades que evitan reflow */
.elemento-animado {
  transform: translateX(100px);  /* Mejor que left: 100px */
  opacity: 0.8;                  /* Mejor que visibility */
  will-change: transform;        /* Avisa al navegador sobre animaciones */
}

/* Agrupación de cambios visuales */
.optimizado {
  /* Usar la propiedad compuesta */
  transform: translateX(10px) scale(1.2) rotate(45deg);
  
  /* En lugar de propiedades individuales */
  /* transform: translateX(10px); */
  /* transform: scale(1.2); */
  /* transform: rotate(45deg); */
}
```

#### Mejores Prácticas de Rendimiento

##### Selectores Eficientes
```css
/* Evitar selectores profundamente anidados */
/* ❌ Malo */
.header nav ul li a span { color: blue; }

/* ✅ Bueno */
.nav-link-text { color: blue; }
```

##### Optimización de Animaciones
```css
.animacion-optimizada {
  /* Usar propiedades que solo afecten a la composición */
  transform: translateZ(0);  /* Fuerza la aceleración por hardware */
  backface-visibility: hidden;
  perspective: 1000px;
}

@keyframes slide-optimizado {
  from { transform: translateX(0); }
  to { transform: translateX(100px); }
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento en dispositivos de gama baja
- Reducción del consumo de batería en móviles
- Mejora en los tiempos de carga inicial
- Experiencia de usuario más fluida
- Mejor posicionamiento SEO por velocidad

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---

#### View Timeline y Scroll-driven Animations
```css
/* Definir una línea de tiempo basada en scroll */
.elemento-animado {
  view-timeline-name: --elemento-scroll;
  view-timeline-axis: block;
  animation-timeline: --elemento-scroll;
  animation-name: aparecer;
}

@keyframes aparecer {
  from { opacity: 0; transform: translateY(50px); }
  to { opacity: 1; transform: translateY(0); }
}
```

#### Efectos Visuales con backdrop-filter
```css
.panel-cristal {
  /* Efecto de cristal esmerilado */
  backdrop-filter: blur(10px) saturate(180%);
  background-color: rgba(255, 255, 255, 0.5);
}

.panel-oscuro {
  /* Efecto oscuro con ajuste de contraste */
  backdrop-filter: blur(5px) brightness(70%);
  background-color: rgba(0, 0, 0, 0.3);
}
```

#### Blend Modes Avanzados
```css
.imagen-mezclada {
  /* Mezcla de colores con el fondo */
  mix-blend-mode: overlay;
}

.contenedor-mezcla {
  /* Mezcla de capas dentro del contenedor */
  background-blend-mode: multiply;
  background-image: 
    linear-gradient(45deg, #ff6b6b, #4ecdc4),
    url('textura.jpg');
}
```

#### Casos de Uso Prácticos

##### Animaciones de Scroll Suaves
```css
/* Revelación progresiva de contenido */
.seccion-contenido {
  view-timeline-name: --revelar-seccion;
  view-timeline-axis: block;
  animation: revelarContenido linear both;
  animation-timeline: --revelar-seccion;
}

@keyframes revelarContenido {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}
```

##### Efectos de Superposición Modernos
```css
.tarjeta-moderna {
  /* Efecto de superposición con degradado */
  position: relative;
  overflow: hidden;
}

.tarjeta-moderna::before {
  content: '';
  position: absolute;
  inset: 0;
  background: linear-gradient(45deg, 
    rgba(255,255,255,0.1),
    rgba(255,255,255,0.5));
  backdrop-filter: blur(5px);
  mix-blend-mode: overlay;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento que las animaciones basadas en JavaScript
- Mayor control sobre efectos visuales complejos
- Compatibilidad progresiva con navegadores modernos
- Reducción de la dependencia de librerías externas
- Optimización automática por el navegador

---

### 7. CSS Interactivity sin JavaScript

CSS moderno ofrece poderosas características para crear interactividad sin necesidad de JavaScript, permitiendo interfaces dinámicas y responsivas con puro CSS.

#### Selectores de Interactividad Avanzados
```css
/* Efectos hover con propagación */
.card:hover > .card-content {
  transform: scale(1.05);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Manejo de foco en formularios */
.form-group:focus-within {
  background: var(--highlight-color);
  border-color: var(--accent-color);
}

/* Navegación con :target */
.tab:target {
  display: block;
  animation: fadeIn 0.3s ease-in;
}
```

#### Scroll Snap para Carruseles
```css
.carousel-container {
  scroll-snap-type: x mandatory;
  overflow-x: auto;
  display: flex;
  -webkit-overflow-scrolling: touch;
}

.carousel-slide {
  scroll-snap-align: start;
  flex: 0 0 100%;
  height: 300px;
  /* Previene el scroll en Safari */
  scroll-snap-stop: always;
}
```

#### Personalización de Elementos Nativos
```css
/* Personalización de checkboxes y radios */
.custom-form {
  accent-color: var(--brand-color);
}

/* Estilizado de scrollbars */
.custom-scroll {
  scrollbar-width: thin;
  scrollbar-color: var(--thumb-color) var(--track-color);
}

/* Estilizado de selección de texto */
::selection {
  background-color: var(--brand-color);
  color: white;
}
```

#### Casos de Uso Prácticos

##### Menú Desplegable sin JavaScript
```css
.dropdown {
  position: relative;
}

.dropdown-toggle:focus + .dropdown-menu,
.dropdown-menu:hover {
  display: block;
  opacity: 1;
  transform: translateY(0);
}

.dropdown-menu {
  position: absolute;
  opacity: 0;
  transform: translateY(-10px);
  transition: all 0.3s ease;
}
```

##### Galería de Imágenes Interactiva
```css
.gallery {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}

.gallery-item:hover {
  z-index: 1;
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

.gallery-item:focus-within {
  outline: 3px solid var(--accent-color);
  outline-offset: 3px;
}
```

#### Ventajas y Consideraciones
- Mejor rendimiento al evitar JavaScript
- Menor consumo de recursos del navegador
- Comportamiento nativo y accesible
- Compatibilidad con gestos táctiles
- Degradación elegante en navegadores antiguos

---
