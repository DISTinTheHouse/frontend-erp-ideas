# Diagnóstico Visual y Sistema de Diseño - ERP/CRM Premium

## 1. Diagnóstico Visual del Estado Actual

### Fortalezas
- **Base Sólida**: La estructura HTML es semántica y el uso de Tailwind CSS es correcto.
- **Modo Oscuro**: La implementación del modo oscuro (`dark:`) está bien lograda y es funcional.
- **Layout General**: La disposición Sidebar + Topbar + Content es estándar y efectiva para aplicaciones empresariales.
- **Tipografía**: La combinación de *Inter* (UI) y *Poppins* (Display/Headings) aporta modernidad y legibilidad.

### Áreas de Mejora Identificadas (y Abordadas)
- **Consistencia de Marca**: Existía una mezcla de acentos (Sky, Blue, Violet, Rose) que diluía la identidad. Se ha unificado todo bajo la paleta **Rose/Brand**.
- **Jerarquía Visual**: Faltaba profundidad en el dashboard. Se añadieron sombras suaves (`shadow-soft`), gradientes sutiles y mejores contrastes en las tarjetas.
- **Feedback de Usuario**: Los estados `hover`, `focus` y `active` eran inconsistentes. Se han estandarizado con transiciones suaves y efectos de escala/color.
- **Densidad de Información**: Las tablas y listas eran demasiado genéricas. Se optimizó el espaciado (`p-3` vs `p-4`) y se añadieron badges y micro-interacciones para mejorar la densidad sin saturar.
- **Navegación Móvil**: El menú móvil era básico. Se mejoró con un *drawer* lateral con backdrop blur.

---

## 2. Sistema de Diseño (Design System)

### Paleta de Colores (Brand: Rose)
Se utiliza una paleta extendida de Rose como color primario para acciones, acentos y estados activos.

```javascript
colors: {
    brand: {
        50: '#fff1f2',  // Fondos muy claros (hover, badges)
        100: '#ffe4e6', // Bordes sutiles
        500: '#f43f5e', // Color Principal (Botones, Iconos, Links)
        600: '#e11d48', // Hover de botones, Textos fuertes
        700: '#be123c', // Bordes oscuros, Estados activos
        900: '#881337', // Textos muy oscuros o fondos de acento en dark mode
    },
    slate: { ... } // Escala de grises para textos y fondos neutros
}
```

### Tipografía
- **Headings (Títulos)**: *Poppins* (Pesos: 500, 600, 700). Para tarjetas, encabezados de sección y métricas clave.
- **Body (Cuerpo)**: *Inter* (Pesos: 300, 400, 500). Para tablas, formularios y texto general. Alta legibilidad en tamaños pequeños.

### Espaciado y Radio
- **Radio de Borde**:
  - `rounded-xl`: Tarjetas, Modales, Dropdowns.
  - `rounded-lg`: Botones, Inputs, Badges.
  - `rounded-full`: Avatares, Status Indicators, Icon buttons.
- **Padding**:
  - Contenedores principales: `p-6` o `p-8`.
  - Tarjetas: `p-5` o `p-6`.
  - Celdas de tabla: `px-6 py-3` (Header), `px-6 py-4` (Body).

### Sombras y Profundidad
- **Shadow Soft**: `0 4px 20px -2px rgba(0, 0, 0, 0.05)` (Para tarjetas en light mode).
- **Glow**: `0 0 15px rgba(244, 63, 94, 0.3)` (Para elementos de acento en dark mode).
- **Glassmorphism**: `backdrop-blur-xl bg-white/80` (Para Topbar y Drawers).

---

## 3. Componentes Reutilizables

### Botones
- **Primario**: `bg-brand-600 text-white hover:bg-brand-500 shadow-lg shadow-brand-600/20`
- **Secundario**: `bg-white dark:bg-slate-800 text-slate-700 dark:text-slate-200 border border-slate-200 dark:border-slate-700 hover:bg-slate-50 dark:hover:bg-slate-700`
- **Ghost/Icon**: `text-slate-400 hover:text-brand-500 hover:bg-brand-50 dark:hover:bg-brand-500/10`

### Tarjetas (KPIs y Contenedores)
```html
<div class="bg-white dark:bg-slate-900 border border-slate-200 dark:border-white/5 rounded-xl shadow-sm hover:shadow-lg transition-all duration-300">
    <!-- Contenido -->
</div>
```

### Tablas (Data Grids)
- **Header**: `bg-slate-50/50 dark:bg-slate-800/20 text-xs uppercase tracking-wider font-bold text-slate-500`.
- **Filas**: `hover:bg-slate-50 dark:hover:bg-white/[0.02] transition-colors border-b border-slate-100 dark:border-white/5`.
- **Badges**: `px-2.5 py-1 rounded-md text-xs font-medium bg-brand-50 dark:bg-brand-500/10 text-brand-600 dark:text-brand-400`.

---

## 4. Nuevas Pantallas Sugeridas (Roadmap)

Para completar la experiencia CRM, se recomienda desarrollar las siguientes vistas:

1.  **Prospectos (Kanban/List)**: Vista dedicada a la gestión de leads con filtros avanzados y estados.
2.  **Detalle de Prospecto (360°)**: Perfil completo con timeline de actividad, notas, correos y tareas asociadas.
3.  **Pipeline de Oportunidades**: Vista visual de etapas de venta (drag & drop).
4.  **Calendario de Actividades**: Vista mensual/semanal de citas y tareas.
5.  **Catálogo de Productos**: Vista de grid/lista con imágenes y stock para selección rápida en pedidos.
6.  **Configuración de Equipo**: Gestión de usuarios, roles y metas comerciales.

---

## 5. Recomendaciones Técnicas (HTML + Tailwind)

1.  **Componentes**: Si es posible, migrar a un framework de componentes (React, Vue, Alpine.js) para evitar repetir clases. Si se mantiene en HTML puro, usar un sistema de plantillas o componentes de servidor.
2.  **Dark Mode Strategy**: Usar siempre la clase `dark:` junto con colores semánticos (`bg-slate-900` en lugar de negros puros `#000`) para reducir la fatiga visual.
3.  **Accesibilidad**: Asegurar contraste suficiente en los textos `text-slate-500` sobre fondos oscuros. Usar etiquetas `aria-label` en botones de solo icono.
4.  **Performance**: Mantener el uso de SVGs inline optimizados o sprites para iconos.

## 6. Ideas "Premium" Implementadas

- **Micro-Sparklines**: Gráficos pequeños en tarjetas de KPI para mostrar tendencia sin ocupar espacio.
- **Ambient Glow**: Fondos con gradientes radiales sutiles para dar profundidad al modo oscuro.
- **Sticky Headers**: Cabeceras de tabla y página fijas para mantener el contexto al hacer scroll.
- **Interactive States**: Feedback visual inmediato al interactuar con cualquier elemento clickeable.
