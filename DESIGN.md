# Design System & Guidelines (Inspirado en Designeer.xyz)

Documento base del sistema de diseño para la aplicación, estructurado de acuerdo con los principios de la skill **`impeccable`** y modelado a partir de la inspección técnica de **[designeer.xyz](https://designeer.xyz)**.

---

## 1. Filosofía Visual y Modo de Interfaz

- **Modo:** **Operate / Dashboard SaaS refinado.**
  - Alta densidad de información con excelente legibilidad y mínimo ruido visual.
  - Superficies con micro-elevaciones, bordes translúcidos limpios (`border-line`) y fondos mate (*wash / well*).
  - Efectos visuales de superficie pulida: `backdrop-blur`, sombras suaves (*float shadow*) y píldoras interactivas.

---

## 2. Sistema de Tokens de Color

El sistema utiliza nombres semánticos de superficies y tintas, funcionando tanto en tema claro como en tema oscuro.

### Modo Claro (Light Mode)
- **`--page`**: `#ffffff` (Lienzo principal de la aplicación).
- **`--well`**: `#f2f2f3` (Fondos de contenedores, inputs y barras laterales secundarias).
- **`--raised`**: `#ffffff` (Tarjetas flotantes, dropdowns, modales).
- **`--wash`**: `rgba(0, 0, 0, 0.035)` (Fondos sutiles interactivos / hover ligero).
- **`--wash-hover`**: `rgba(0, 0, 0, 0.055)` (Hover en elementos de lista y botones planos).
- **`--ink`**: `#18181b` (Texto principal de alto contraste - `zinc-900`).
- **`--ink-2`**: `#5d5d66` (Texto secundario, etiquetas y encabezados tenues).
- **`--ink-3`**: `#6b6b73` (Texto terciario, metadatos, placeholders).
- **`--line`**: `rgba(0, 0, 0, 0.07)` (Bordes sutiles divisores de tarjeta y tabla).
- **`--line-strong`**: `rgba(0, 0, 0, 0.16)` (Bordes de inputs activos y botones secundarios).

### Modo Oscuro (Dark Mode)
- **`--page`**: `#121212` (Fondo general profundo).
- **`--well`**: `#1b1b1e` (Sidebar, paneles agrupadores).
- **`--raised`**: `#1f1f22` (Tarjetas y modales elevados).
- **`--wash`**: `rgba(255, 255, 255, 0.05)` (Hover de botones neutros).
- **`--wash-hover`**: `rgba(255, 255, 255, 0.08)`
- **`--ink`**: `#fafafa` (Texto blanco mate de alta legibilidad).
- **`--ink-2`**: `#a8a8ad` (Texto secundario tenue).
- **`--ink-3`**: `#8b8b92` (Metadatos).
- **`--line`**: `rgba(255, 255, 255, 0.08)`
- **`--line-strong`**: `rgba(255, 255, 255, 0.18)`

### Acentos Semánticos
- **Brand / Acción primaria:** `indigo-600` (`#4f46e5`) o `zinc-900` (`#18181b`) con texto de contraste alto.
- **Éxito / Stock alto:** `emerald-600` / `green-500`.
- **Alerta / Stock bajo:** `amber-500` (`#fcbb00`).
- **Peligro / Destructivo / Agotado:** `rose-500` / `rose-600`.

---

## 3. Tipografía y Jerarquía

- **Sans Principal:** `Inter`, `system-ui`, `-apple-system`, `sans-serif`.
- **Monoespaciada y Cifras (Mandatorio para POS):** `font-mono tabular-nums` en precios, códigos de barras, SKUs, inventarios y totales monetarios.
- **Escala de tamaños:**
  - **Títulos:** `text-2xl` / `text-xl` `font-semibold tracking-tight text-ink`.
  - **Subtítulos y grupos:** `text-sm` `font-medium text-ink-2`.
  - **Cuerpo / Controles:** `text-sm` `text-ink`.
  - **Metadatos y badges:** `text-xs` `text-ink-3`.

---

## 4. Componentes y Patrones de Interfaz

### 1. Barra de Navegación / Sidebar
- Fondo sutil `bg-well` o `bg-page/80 backdrop-blur-md` con borde lateral `border-r border-line`.
- Enlaces de navegación tipo píldora (`rounded-lg` o `rounded-full`) con transición suave en hover `hover:bg-wash-hover hover:text-ink`.

### 2. Tarjetas y Paneles (`panel-surface`)
- Fondo `bg-raised`, borde `border border-line`, esquinas redondeadas `rounded-xl`.
- Sombra flotante delicada: `shadow-[0_1px_3px_0_rgba(0,0,0,0.04),0_1px_2px_-1px_rgba(0,0,0,0.04)]`.

### 3. Tablas de Inventario y Ventas
- Encabezados: `text-xs font-semibold text-ink-2 uppercase tracking-wider bg-well/50 border-b border-line`.
- Filas: `hover:bg-wash transition-colors border-b border-line/60`.
- Celdas numéricas alineadas a la derecha con `font-mono tabular-nums`.

### 4. Formularios e Inputs
- Campos de entrada con fondo `bg-page`, borde `border border-line-strong`, redondeo `rounded-lg`, foco con anillo limpio `focus:ring-2 focus:ring-ink/10 focus:border-ink`.
- Mensajes de error accesibles con `role="alert"` y clase `text-rose-600 text-xs mt-1`.

---

## 5. Craft Floor (Reglas de Calidad Impeccable)

1. **Sin bordes negros duros o chillones:** Usar siempre los tokens semánticos `border-line` o `border-line-strong`.
2. **Espaciados consistentes:** Múltiplos de 4px (`gap-2`, `gap-4`, `p-4`, `p-6`).
3. **Estados interactivos completos:** Todo botón y enlace debe tener estilos visibles para `hover`, `active`, `focus-visible` y `disabled:opacity-50`.
4. **Accesibilidad garantizada:** Contraste mínimo WCAG AA en textos y etiquetas asociadas explícitamente a sus campos (`label for="..."`).

