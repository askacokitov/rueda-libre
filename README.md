### 1. Resumen y Objetivos

* **Propósito del proyecto:** Modernizar la plataforma web de *Rueda Libre* migrando la sección de la campaña "Edición Nocturna" desde un entorno basado en Bootstrap hacia una arquitectura moderna, orientada a utilidades con **Tailwind CSS (CLI v4)**.


* **Metas principales:**
* Construir una landing page de alto rendimiento, 100% responsiva (mobile-first) y con soporte nativo para **modo oscuro (`dark:`)**.


* Cumplir estrictamente con criterios de accesibilidad y contraste WCAG (mínimo 4.5:1) utilizando una paleta de colores corporativa unificada.


* Integrar de forma fluida el sitio legacy en Bootstrap v2.0 con la nueva landing en Tailwind mediante navegación cruzada y rutas relativas correctas.


### 2. Definición de Identidad y Marca (Tokens de Color y Tipografía)

* **Tipografías:**
* Títulos: *Montserrat* (Google Fonts, pesos 400 y 700).

* Cuerpo: *Open Sans* (Google Fonts, pesos 400 y 600).

* **Paleta de Colores Corporativos (Definidos en el `@theme` de Tailwind y variables CSS):**
* **Azul Noche** (`#2b2d42`): Color base para modo oscuro y encabezados.
* **Gris Azulado** (`#8d99ae`): Textos secundarios y bordes.
* **Fondo Claro** (`#edf2f4`): Fondos generales en modo claro.
* **Rojo Carmesí** (`#ef233c`): Acentos, precios destacados y botones principales.
* **Verde Ruta** (`#2a9d8f`): Botones secundarios y etiquetas de rutas fáciles.
* **Naranja Pedal** (`#f77f00`): Botones alternativos y alertas.
* **Amarillo Farol** (`#FFD166`): Textos en modo oscuro de alta visibilidad, elementos destacados y la insignia *"★ Más elegido"*.



### 3. Fases de Desarrollo, Tiempos y Pruebas

#### Fase 1: Entorno y Configuración Base

* **Tecnologías:** Node.js, Tailwind CLI v4, Google Fonts.
* **Acciones:** Configuración del archivo `input.css` asegurando el orden correcto de las directivas `@import` (colocando fuentes y `@import "tailwindcss";` en orden estricto) y definición del bloque `@theme`.


* **Optimización y Compilación:** Uso de la opción `--minify` para generar un archivo `output.css` de producción sumamente ligero (menor a 20 KB frente a los más de 100-200 KB combinados de Bootstrap CSS + JS Bundle).

#### Fase 2: Componentes y Optimización (`@apply`)

* **Conteo de clases repetidas:** Los botones y componentes visuales se repetían hasta en 12 lugares diferentes con idénticas propiedades.
* **Uso de directivas:** Se aplicó `@apply` con moderación dentro de la capa `@layer components` para encapsular exactamente tres clases reutilizables:
* `.btn-marca-principal` (Botones de acción principal en rojo).
* `.btn-marca-secundario` (Botones de acción secundaria en verde).
* `.btn-marca-alternativo` (Botones alternativos en naranja).



#### Fase 3: Maquetación de la Landing y Secciones Clave

* **Hero Section:** Mensaje de impacto, llamado a la acción (`#rutas`) e insignia de cupos limitados.


* **Sección de Rutas:** Cuadrícula responsiva (`grid-cols-1 sm:grid-cols-2 lg:grid-cols-3`) con las 3 rutas oficiales (*Luces del Centro*, *Miradores de la Ciudad* y *Luna en Las Palmas*), incluyendo imágenes, distancias, duraciones y precios.


* **Sección "¿Cómo funciona?":** Guía secuencial de cuatro pasos con tarjetas informativas.


* **Sección "Planes Rueda Nocturna" (Requerimiento exprés):**
* *Estructura:* Cuadrícula adaptable con tarjetas de igual altura (`items-stretch`, `flex flex-col h-full`) y distribución uniforme de beneficios mediante `flex-grow`.


* *Plan Destacado:* El **Plan Pareja** ($99.000) se destacó visualmente con un borde de color *Amarillo Farol*, fondo específico en modo oscuro (`dark:bg-[#151b2b]`), un anillo luminoso y la etiqueta flotante superior **"★ Más elegido"**, sin alterar la simetría de la grilla.





#### Fase 4: Formulario de Inscripción Accesible y Validado

* **Semántica:** Implementación estricta de etiquetas semánticas (`<form>`, `<fieldset>`, `<legend>`, `<label>`, `<select>`, `<input>`, `<checkbox>`).


* **Validación Nativa:**
* Nombre: Obligatorio, mínimo 3 caracteres (`required minlength="3"`).
* Correo: Obligatorio de tipo email (`required`).
* Celular: Obligatorio, exactamente 10 dígitos empezando por 3 (`required pattern="3\d{9}" maxlength="10"`).
* Acompañantes: Rango permitido de 0 a 3 (`required min="0" max="3"`).
* Términos y condiciones: Casilla de aceptación obligatoria (`required`).


* **Accesibilidad:** Navegación fluida por completo utilizando únicamente la tecla `Tab` con indicadores de foco visibles (`focus:ring`).

---

### 4. Tabla Comparativa: Bootstrap v2.0 vs. Tailwind CSS v4.0

| Criterio de Comparación | Bootstrap (Framework basado en componentes) | Tailwind CSS (Framework Utility-First) |
| --- | --- | --- |
| **Curva de Aprendizaje** | Rápida al inicio por usar componentes predefinidos (`btn`, `card`), pero compleja al requerir modificar estilos base o anular reglas. | Requiere aprender la nomenclatura de utilidades atómicas, pero otorga control total y directo sobre cada regla visual sin salir del HTML. |
| **Personalización** | Exige sobrescribir variables Sass/CSS globales o usar selectores complejos con `!important` para amoldarse a la identidad visual. | Altamente flexible y modular mediante el bloque `@theme` y directivas como `@apply`, adaptándose de forma nativa a cualquier guía de marca. |
| **Tamaño Final (Assets)** | Mayor peso en red al descargar componentes y clases pregeneradas que a menudo no se usan (CSS + JS Bundle > 100 KB). | Altamente optimizado gracias al sistema de *tree-shaking* y minificación (`--minify`), generando un archivo final extremadamente ligero (< 20 KB). |
| **Casos de Uso Ideales** | Prototipado rápido y estandarizado donde la velocidad de desarrollo prima sobre la unicidad visual del diseño. | Aplicaciones y sitios web modernos con identidades de marca únicas, diseño mobile-first complejo, modo oscuro nativo y alto rendimiento. |

* **Recomendación Justificada para Rueda Libre:** Se recomienda la **adopción definitiva de Tailwind CSS** para el ecosistema de *Rueda Libre*, ya que permitió unificar con precisión milimétrica la paleta corporativa, integrar un modo oscuro impecable, reducir drásticamente el peso de transferencia en red y garantizar una experiencia móvil robusta.

---

### 5. Integración del Ecosistema y Despliegue

* **Conexión Bootstrap ↔ Tailwind:**
* En el sitio tradicional de Bootstrap (`index.html`, `tarifas.html`, `reservas.html`), se añadió el enlace de navegación **"Rueda Nocturna"** y una cuarta diapositiva promocional en el carrusel principal que redirige directamente a la landing.


* En la landing de Tailwind (`nocturna/index.html`), el logotipo dirige al inicio (`#hero`) y se incorporó un botón explícito de **"Reserva tu bici"** que conecta correctamente con el módulo de reservas del sitio principal mediante rutas relativas (`../paginas/reservas.html`).


* **Verificación de Enlaces:** Cero errores 404 tanto en entorno local (Live Server) como en el despliegue público en GitHub Pages.
