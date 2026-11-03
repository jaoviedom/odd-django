# Django Fullstack - Guía Técnica para Organic Driven Development (ODD)

Este documento define las directrices y estándares de desarrollo para trabajar en este proyecto (**Django 5/6 + Python 3.12+ + Pytest-Django / Django Templates**), en estricta coherencia con los principios de **Organic Driven Development (ODD)** y el flujo de trabajo `/backlog` → `/story` → `/pair`.

---

## 1. Principios ODD Aplicados a Django

1. **No inventar requerimientos:** No crear modelos, campos, vistas, formularios ni endpoints que no estén en los criterios de aceptación acordados de la historia activa.
2. **Lo más simple que funcione (Simple Design / YAGNI):** Empezar con el mecanismo estándar más directo de Django (modelos simples, vistas estándar, Django Forms). No introducir capas adicionales (`services/`, `actions/`, middleware personalizado) "por si acaso"; sugerir refactorizaciones solo cuando una señal concreta en el código lo justifique.
3. **Corte vertical y pequeño:** Cada historia atraviesa todas las capas necesarias (modelo/migración, vista/formulario, plantilla) para entregar valor real de punta a punta.
4. **Sugerir, no decidir:** Los patrones arquitectónicos, optimizaciones prematuras o refactorizaciones complejas se sugieren al usuario; la decisión final es siempre del usuario (Navigator).
5. **Checkpoints explícitos (Paso a paso en Pair):** Un test a la vez → mostrar que falla (rojo) → código mínimo (~50 líneas o máx. 3 archivos) → mostrar que pasa (verde) → parar y pedir confirmación.

---

## 2. Convenciones de Backend (Django & Python)

### Modelos y ORM
- Definir siempre `__str__()` descriptivo.
- Establecer `on_delete` explícito en claves foráneas (`CASCADE`, `PROTECT`, `SET_NULL`, etc.).
- Definir `related_name` semántico en relaciones inversas.
- Prevenir activamente consultas N+1: usar `select_related(...)` para ForeignKey/OneToOne y `prefetch_related(...)` para ManyToMany/Reverse relations en vistas y consultas complejas.
- Mutaciones críticas que involucren múltiples modelos relacionados o consistencia financiera deben encapsularse con `@transaction.atomic`.

### Vistas y Enrutamiento
- Rutas organizadas y modularizadas por aplicación (`<app>/urls.py`) con `app_name = '<app>'` y nombres explícitos de ruta (`path('...', view, name='nombre')`).
- Mantener las vistas enfocadas en el flujo HTTP (autenticación, orquestación de formulario/datos y renderizado/redirección).
- Validación de entradas mediante formularios estándar de Django (`forms.Form` o `forms.ModelForm`).

---

## 3. Convenciones de Frontend (Django Templates + Tailwind CSS Local + Skill Impeccable)

- **Uso de la Skill Impeccable para Diseño y Frontend:**
  - Todo trabajo de interfaz visual (diseño, rediseño, maquetación, paleta, tipografía, microinteracciones, estados vacíos, componentes o revisión de UX) debe apoyarse en la skill **`impeccable`** (`.agent/skills/impeccable/`).
  - Seguir sus directrices de diseño (jerarquía, legibilidad, modo de interfaz, craft floor y tokens en `DESIGN.md`).
  - Utilizar sus herramientas y referencias para auditar la accesibilidad (WCAG 2.1 AA), responsive design y calidad visual antes de dar por buena una plantilla.

- **Uso Mandatorio de Tailwind CSS Local:**
  - Tailwind CSS **siempre debe compilarse y servirse localmente** (nunca mediante CDN en producción ni entornos finales).
  - Si no está inicializado en el proyecto, el agente debe verificar e inicializar el entorno local de Tailwind:
    1. Archivo `package.json` en la raíz con el script de build y watch (usando `@tailwindcss/cli`).
    2. Archivo de entrada CSS (ej. `static/css/input.css` con `@import "tailwindcss";` para Tailwind v4 o `@tailwind base; components; utilities;` para v3).
    3. Archivo compilado de salida generado localmente (ej. `static/css/output.css`).
    4. Comando para compilar en desarrollo: `npm run dev` (o `npx @tailwindcss/cli -i static/css/input.css -o static/css/output.css --watch`).
    5. Comando para compilar en producción: `npm run build` (o `npx @tailwindcss/cli -i static/css/input.css -o static/css/output.css --minify`).
- **Seguridad en Formularios:** Todo formulario con método POST debe incluir obligatoriamente el token `{% csrf_token %}`.
- **Herencia de Plantillas:** Reutilizar el layout base común (`base.html`), enlazando el archivo CSS local compilado (`{% static 'css/output.css' %}`).
- **Mensajería:** Asegurar que los mensajes del framework de Django (`messages.success`, `messages.error`, etc.) se muestren apropiadamente en las vistas con estilos acordes.
- **Accesibilidad básica:** Inputs asociados a `<label for="...">`, y mensajes de error visibles vinculados a los campos.
- **Tipografía tabular:** Usar clases monoespaciadas/tabulares (`font-mono tabular-nums`) para precios, totales y códigos cuando aplique.

---

## 4. Testing y Ciclo TDD (Pytest-Django / Django TestCase)

- **Ubicación:** `tests/` o `<app>/tests/`.
- **Enfoque de prueba:** Probar comportamiento observable a través de la interfaz pública (endpoints, vistas, formularios, modelos), no detalles de implementación interna.
- **Valores esperados:** El valor esperado proviene del criterio de aceptación acordado, **nunca** calculado con la misma lógica que el código productivo.
- **Inmutabilidad de pruebas acordadas:** Nunca modificar o relajar las aserciones de un test para forzar un pase verde. La solución debe corregirse en el código productivo.

---

## 5. Control de Calidad y Cierre de Paso

Antes de dar un paso o tarea por cerrada, verificar en la terminal integrada:
1. `python manage.py check` (sin errores de configuración de sistema).
2. `python manage.py makemigrations --check --dry-run` (sin migraciones desincronizadas).
3. `pytest` o `python manage.py test` (todos los tests en verde).

---

## 6. Prohibiciones Explícitas

1. **NO** escribir código sin antes haber aprobado el listado de tests con el usuario en `/pair`.
2. **NO** crear archivos o abstracciones adicionales (ej. servicios, repositorios, factories) antes de que la solución simple lo requiera.
3. **NO** editar o relajar tests aprobados para ocultar un fallo.
4. **NO** hacer commits de git de forma autónoma.
