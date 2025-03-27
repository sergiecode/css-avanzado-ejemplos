# CSS Moderno 

---

# Selectores y funciones avanzadas en CSS

### 1. :has() - El selector padre

#### Definición
El selector `:has()` es una pseudo-clase que permite seleccionar elementos basándose en sus elementos hijos o descendientes. Es conocido como el "selector padre" porque finalmente nos permite seleccionar elementos padres basándonos en sus hijos.

#### Para qué sirve
- Permite seleccionar elementos contenedores basándose en su contenido
- Facilita la modificación de estilos de elementos padres según sus hijos
- Reduce la necesidad de clases adicionales o JavaScript para manipular elementos padres

#### Ejemplos
```css
/* Selecciona párrafos que contienen imágenes */
p:has(img) {
    display: flex;
    align-items: center;
}

/* Estiliza el contenedor cuando tiene elementos específicos */
.container:has(.elemento-especial) {
    background-color: #f0f0f0;
    padding: 20px;
}

/* Modifica el diseño cuando hay múltiples elementos */
.galeria:has(> img:nth-child(3)) {
    grid-template-columns: repeat(3, 1fr);
}
```

### 2. :is(), :where() y :not()

#### Definición
Estos selectores son pseudo-clases que permiten simplificar y optimizar la escritura de selectores complejos en CSS:
- `:is()`: Agrupa selectores y mantiene la especificidad del selector más específico
- `:where()`: Similar a `:is()` pero con especificidad cero
- `:not()`: Selecciona elementos que no coinciden con el selector dado

#### Para qué sirve
- Reduce la repetición de código en selectores complejos
- Mejora la legibilidad del código CSS
- Permite crear reglas más flexibles y mantenibles

#### Ejemplos
```css
/* Usando :is() para simplificar selectores */
:is(header, main, footer) p {
    margin-bottom: 1rem;
}

/* Usando :where() para estilos de baja especificidad */
:where(article, section) > h2 {
    color: #333;
}

/* Combinando :not() con otros selectores */
.menu-item:not(.active) {
    opacity: 0.7;
}
```

### 3. :nth-child(n of selector)

#### Definición
Esta pseudo-clase permite seleccionar elementos específicos de un tipo particular dentro de un conjunto de hermanos, utilizando una expresión numérica.

#### Para qué sirve
- Selecciona elementos con mayor precisión
- Permite filtrar elementos por tipo antes de aplicar la fórmula nth-child
- Facilita la creación de patrones de diseño complejos

#### Ejemplos
```css
/* Selecciona el segundo párrafo entre elementos p */
:nth-child(2 of p) {
    font-weight: bold;
}

/* Estiliza cada tercer elemento de tipo .card */
:nth-child(3n of .card) {
    margin-right: 0;
}

/* Aplica estilos al primer elemento de tipo .imagen */
:nth-child(1 of .imagen) {
    border: 2px solid #blue;
}
```

---

# Container Queries(Reemplazo de Media Queries)

### 1. Diferencia entre @media queries y @container queries

#### Definición
Mientras que los Media Queries se basan en las dimensiones de la ventana del navegador, los Container Queries permiten aplicar estilos basados en el tamaño del contenedor padre más cercano.

#### Para qué sirve
- Permite crear componentes verdaderamente reutilizables y adaptables
- Facilita el diseño responsivo a nivel de componente
- Mejora la modularidad y la mantenibilidad del código

#### Ejemplos
```css
/* Definiendo un contenedor */
.card-container {
    container-type: inline-size;
    container-name: card;
}

/* Aplicando estilos basados en el tamaño del contenedor */
@container card (min-width: 400px) {
    .card {
        display: grid;
        grid-template-columns: 200px 1fr;
    }
}
```

### 2. Implementación de container queries en proyectos responsivos

#### Definición
Los Container Queries requieren la definición explícita de contenedores de consulta mediante la propiedad container-type, permitiendo que los elementos hijos respondan al tamaño de su contenedor.

#### Para qué sirve
- Crea layouts más flexibles y adaptables
- Permite reutilizar componentes en diferentes contextos
- Simplifica el mantenimiento de componentes responsivos

#### Ejemplos
```css
/* Configuración básica de un contenedor */
.sidebar {
    container-type: inline-size;
}

/* Adaptando componentes según el contenedor */
@container (min-width: 300px) {
    .widget {
        grid-template-columns: repeat(2, 1fr);
        gap: 1rem;
    }
}
```

### 3. Ejemplo práctico: Diseñar un componente adaptable

#### Definición
Un componente adaptable es aquel que modifica su diseño y comportamiento basándose en el espacio disponible en su contenedor, independientemente del viewport.

#### Para qué sirve
- Crea interfaces más flexibles y reutilizables
- Mejora la experiencia de usuario en diferentes contextos
- Facilita el mantenimiento y la escalabilidad

#### Ejemplos
```css
/* Configuración del contenedor principal */
.product-card {
    container-type: inline-size;
    container-name: product;
}

/* Estilos base */
.product-content {
    display: flex;
    flex-direction: column;
}

/* Adaptaciones según el tamaño del contenedor */
@container product (min-width: 500px) {
    .product-content {
        flex-direction: row;
        align-items: center;
    }
    
    .product-image {
        width: 40%;
    }
    
    .product-info {
        width: 60%;
        padding-left: 2rem;
    }
}
```

---

# Variables CSS y mejoras en custom properties

### 1. Uso avanzado de var(), calc(), clamp(), min(), max()

#### Definición
Estas funciones son herramientas fundamentales para realizar cálculos y manipular valores en CSS de manera dinámica y flexible:
- `var()`: Permite usar variables CSS personalizadas
- `calc()`: Realiza operaciones matemáticas
- `clamp()`: Define un valor entre un mínimo y máximo
- `min()` y `max()`: Seleccionan el valor menor o mayor entre varios

#### Para qué sirve
- Crea diseños más dinámicos y adaptables
- Permite realizar cálculos complejos directamente en CSS
- Facilita la creación de layouts responsivos sin media queries

#### Ejemplos
```css
:root {
    --spacing-base: 1rem;
    --font-size-base: 16px;
}

.contenedor {
    /* Usando calc() con variables */
    padding: calc(var(--spacing-base) * 2);
    
    /* Usando clamp() para tamaños responsivos */
    width: clamp(300px, 80%, 1200px);
    
    /* Combinando min() y max() */
    font-size: max(var(--font-size-base), min(2vw, 24px));
}
```

### 2. Nueva API @property para definir variables con tipos específicos

#### Definición
La API @property permite definir propiedades personalizadas con tipos de datos específicos, valores iniciales y comportamientos de animación.

#### Para qué sirve
- Define variables CSS con tipos de datos estrictos
- Permite animaciones suaves entre valores
- Mejora el control sobre las propiedades personalizadas

#### Ejemplos
```css
/* Definiendo una propiedad numérica animable */
@property --rotacion {
    syntax: '<angle>';
    initial-value: 0deg;
    inherits: false;
}

/* Definiendo una propiedad de color */
@property --color-principal {
    syntax: '<color>';
    initial-value: #007bff;
    inherits: true;
}
```

### 3. Ejemplo práctico: Crear un tema dinámico con variables

#### Definición
Un tema dinámico utiliza variables CSS para modificar la apariencia de una interfaz de manera consistente y mantenible.

#### Para qué sirve
- Facilita la implementación de temas claros y oscuros
- Permite cambios globales de estilo con pocas modificaciones
- Mejora la consistencia del diseño

#### Ejemplos
```css
/* Definición de variables para el tema */
:root {
    --color-fondo: #ffffff;
    --color-texto: #333333;
    --color-primario: #0066cc;
    --espaciado: 1rem;
}

/* Tema oscuro */
[data-theme="dark"] {
    --color-fondo: #1a1a1a;
    --color-texto: #ffffff;
    --color-primario: #66b3ff;
}

/* Aplicación de variables */
.componente {
    background-color: var(--color-fondo);
    color: var(--color-texto);
    padding: var(--espaciado);
    border: 1px solid var(--color-primario);
}
```

---

# Nuevas funciones CSS de color y accesibilidad

### 1. color-mix() - Mezclando colores en CSS puro

#### Definición
La función color-mix() permite mezclar dos colores directamente en CSS, especificando el espacio de color y el porcentaje de mezcla deseado.

#### Para qué sirve
- Crea variaciones de color sin necesidad de preprocesadores
- Genera paletas de color dinámicas
- Facilita la creación de efectos de color avanzados

#### Ejemplos
```css
.elemento {
    /* Mezcla básica de colores */
    background-color: color-mix(in srgb, #ff0000 50%, #0000ff);
    
    /* Creando un color semi-transparente */
    border-color: color-mix(in srgb, var(--color-primario) 75%, transparent);
    
    /* Mezclando en espacio de color LCH */
    color: color-mix(in lch, #3f0f9c 60%, #d9376e);
}
```

### 2. color-contrast() - Selección automática de colores con buen contraste

#### Definición
La función color-contrast() selecciona automáticamente el color con mejor contraste de una lista de opciones, garantizando la legibilidad.

#### Para qué sirve
- Mejora la accesibilidad automáticamente
- Asegura un contraste adecuado en textos
- Simplifica la creación de interfaces accesibles

#### Ejemplos
```css
.texto {
    /* Selección automática del mejor contraste */
    color: color-contrast(var(--color-fondo) vs
        black, white, #767676);
}

.boton {
    background: var(--color-primario);
    /* Asegurando texto legible */
    color: color-contrast(var(--color-primario) vs
        white, black);
}
```

### 3. Uso de oklch, oklab, hwb() para modelos de color más realistas

#### Definición
Estos son nuevos espacios de color que proporcionan una representación más precisa y perceptualmente uniforme de los colores.

#### Para qué sirve
- Permite crear paletas de color más naturales
- Mejora la precisión en las transiciones de color
- Facilita la creación de esquemas de color accesibles

#### Ejemplos
```css
.elemento {
    /* Usando OKLCH para colores vibrantes */
    background-color: oklch(70% 0.15 340);
    
    /* Transiciones suaves con OKLAB */
    color: oklab(80% -0.02 0.13);
    
    /* Usando HWB para colores intuitivos */
    border-color: hwb(280 10% 20%);
}

/* Gradiente usando OKLCH */
.gradiente {
    background: linear-gradient(
        to right,
        oklch(80% 0.12 30),
        oklch(65% 0.15 180)
    );
}
```

---

# Scroll-driven Animations y efectos visuales CSS avanzados

### 1. view-timeline y animation-timeline: Animaciones basadas en scroll sin JavaScript

#### Definición
Estas propiedades permiten crear animaciones que se ejecutan en función de la posición del scroll, sin necesidad de JavaScript, utilizando el timeline de vista como controlador.

#### Para qué sirve
- Crea animaciones suaves vinculadas al scroll
- Mejora el rendimiento al no depender de JavaScript
- Permite efectos visuales más naturales y fluidos

#### Ejemplos
```css
.elemento {
    animation: aparecer linear;
    animation-timeline: view();
    animation-range: entry 20% cover 50%;
}

@keyframes aparecer {
    from {
        opacity: 0;
        transform: translateY(50px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}
```

### 2. Nuevas opciones para backdrop-filter y blend-mode

#### Definición
Estas propiedades permiten aplicar efectos visuales avanzados a elementos y sus fondos, creando efectos de superposición y mezcla.

#### Para qué sirve
- Crea efectos de desenfoque y filtrado en fondos
- Permite efectos de mezcla entre capas
- Mejora la profundidad visual de interfaces

#### Ejemplos
```css
.modal {
    backdrop-filter: blur(10px) brightness(90%);
    background: rgba(255, 255, 255, 0.1);
}

.imagen-overlay {
    mix-blend-mode: overlay;
    background: linear-gradient(45deg, #ff6b6b, #4ecdc4);
}
```

### 3. Ejemplo práctico: Crear un efecto de animación en scroll

#### Definición
Un efecto de animación en scroll combina diferentes propiedades para crear una experiencia visual interactiva mientras el usuario desplaza la página.

#### Para qué sirve
- Mejora la experiencia de usuario
- Crea transiciones suaves y naturales
- Aumenta el engagement con el contenido

#### Ejemplos
```css
/* Configuración del contenedor */
.scroll-container {
    scroll-timeline-name: --revelar;
    scroll-timeline-axis: block;
}

/* Elemento con animación */
.scroll-elemento {
    opacity: 0;
    transform: translateX(-100px);
    animation: deslizar-entrada linear;
    animation-timeline: --revelar;
    animation-range: entry 10% cover 30%;
}

@keyframes deslizar-entrada {
    from {
        opacity: 0;
        transform: translateX(-100px);
    }
    to {
        opacity: 1;
        transform: translateX(0);
    }
}
```

---

# Optimización de rendimiento con CSS

### 1. Uso de content-visibility para mejorar performance

#### Definición
La propiedad content-visibility permite al navegador omitir el renderizado de elementos que no están en la ventana visible, mejorando significativamente el rendimiento de la página.

#### Para qué sirve
- Reduce el tiempo de carga inicial
- Optimiza el renderizado de contenido fuera de pantalla
- Mejora el rendimiento en páginas largas

#### Ejemplos
```css
.seccion-larga {
    content-visibility: auto;
    contain-intrinsic-size: 0 500px;
}

.componente-pesado {
    content-visibility: auto;
    contain-intrinsic-size: 1000px;
}
```

### 2. Estrategias de carga progresiva y lazy loading de estilos

#### Definición
Técnicas que permiten cargar estilos de manera gradual y bajo demanda, priorizando el contenido visible inicialmente.

#### Para qué sirve
- Mejora el tiempo de carga percibido
- Optimiza el uso de recursos
- Prioriza el contenido crítico

#### Ejemplos
```css
/* Estilos críticos inline */
.header {
    font-display: swap;
    background-image: url(placeholder.jpg);
}

/* Carga diferida de imágenes */
.imagen-diferida {
    loading: lazy;
    background-image: none;
}

@media (min-width: 768px) {
    .imagen-diferida {
        background-image: url(imagen-completa.jpg);
    }
}
```

### 3. Buenas prácticas para minimizar reflows y repaints

#### Definición
Técnicas y estrategias para reducir la cantidad de recálculos de layout y repintados que el navegador debe realizar.

#### Para qué sirve
- Mejora la fluidez de la interfaz
- Reduce el consumo de CPU
- Optimiza la experiencia en dispositivos móviles

#### Ejemplos
```css
/* Usar transform en lugar de propiedades que causan reflow */
.elemento-animado {
    transform: translateX(100px);
    will-change: transform;
}

/* Agrupar cambios de layout */
.contenedor-optimizado {
    contain: layout;
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
}

/* Evitar cálculos frecuentes */
.elemento-fijo {
    position: fixed;
    top: 0;
    left: 0;
    transform: translate3d(0, 0, 0);
    backface-visibility: hidden;
}
```

---

# Interactividad sin JavaScript

### 1. Cómo usar :hover, :focus-within y :target para efectos interactivos

#### Definición
Estas pseudo-clases permiten crear interacciones y efectos visuales sin necesidad de JavaScript, respondiendo a acciones del usuario como hover, focus y navegación por anclas.

#### Para qué sirve
- Crea interacciones fluidas y naturales
- Mejora la accesibilidad de la interfaz
- Reduce la dependencia de JavaScript

#### Ejemplos
```css
/* Menú desplegable con :hover */
.menu-item:hover .submenu {
    opacity: 1;
    transform: translateY(0);
    pointer-events: auto;
}

/* Resaltado de formulario con :focus-within */
.form-group:focus-within {
    background: rgba(0, 123, 255, 0.1);
    border-color: #007bff;
}

/* Modal con :target */
.modal:target {
    display: flex;
    opacity: 1;
}
```

### 2. scroll-snap: Creando carruseles y secciones deslizables sin JS

#### Definición
La propiedad scroll-snap permite crear experiencias de desplazamiento suave y controlado sin necesidad de JavaScript, ideal para carruseles y presentaciones.

#### Para qué sirve
- Crea navegación fluida entre secciones
- Mejora la experiencia de deslizamiento
- Simplifica la implementación de carruseles

#### Ejemplos
```css
/* Contenedor de carrusel */
.carrusel {
    scroll-snap-type: x mandatory;
    overflow-x: scroll;
    display: flex;
}

/* Elementos del carrusel */
.carrusel-item {
    scroll-snap-align: start;
    flex: 0 0 100%;
    width: 100%;
}

/* Navegación vertical con snap */
.pagina-secciones {
    scroll-snap-type: y proximity;
    overflow-y: scroll;
    height: 100vh;
}
```

### 3. Personalizando elementos nativos con accent-color

#### Definición
La propiedad accent-color permite personalizar el color de elementos de formulario nativos como checkboxes, radio buttons y rangos, manteniendo su funcionalidad nativa.

#### Para qué sirve
- Personaliza elementos de formulario nativos
- Mantiene la accesibilidad y usabilidad
- Mejora la consistencia visual

#### Ejemplos
```css
/* Aplicando color de acento global */
:root {
    accent-color: #0066cc;
}

/* Personalizando elementos específicos */
.formulario-especial {
    accent-color: #ff4444;
}

/* Diferentes colores por tipo de input */
input[type="checkbox"] {
    accent-color: #28a745;
}

input[type="range"] {
    accent-color: #17a2b8;
}
```


---
