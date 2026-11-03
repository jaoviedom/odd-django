# Django ODD Starter Template

Plantilla base para proyectos **Django Fullstack** guiados por **Organic Driven Development (ODD)**: desarrollo asistido por IA en pareja, en pequeños pasos verticales, con TDD estricto y sin perder el control de las decisiones arquitectónicas.

Inspirado en los principios de Extreme Programming (XP).

---

## 1. El Flujo de Trabajo ODD

```
/backlog  →  /story  →  /pair
  qué        qué exactamente   cómo
```

| Habilidad / Comando | Propósito | Reglas de Oro |
|---|---|---|
| [`/backlog`](.agent/skills/backlog/SKILL.md) | Convierte una idea o funcionalidad en un backlog de historias de usuario verticales (de una línea). | No inventa requerimientos, no crea tareas técnicas ni estimaciones. |
| [`/story`](.agent/skills/story/SKILL.md) | Toma **una** historia del backlog, define 2–3 criterios de aceptación Given/When/Then y un mini plan (≤5 puntos). | No escribe código. Si requiere más de 3 criterios, propone dividir la historia. |
| [`/pair`](.agent/skills/pair/SKILL.md) | Pair programming: la IA conduce (driver) y tú navegas. Un test → rojo → código mínimo (~50 líneas) → verde → esperar aprobación. | No hace commits, no edita tests para forzar el pase, no agrega extras no solicitados. |

### Principios Fundamentales
- **No inventar requerimientos:** Lo que falte se pregunta; nunca se asume.
- **Lo más simple que funcione (Simple Design / YAGNI):** Cero abstracciones o capas anticipadas "para el futuro".
- **Corte vertical y pasos pequeños:** Cada historia corta todas las capas necesarias; cada paso es un test y ~50 líneas.
- **Sugerir, no decidir:** Las decisiones arquitectónicas, patrones de diseño y refactorizaciones son potestad del usuario (Navigator).
- **Checkpoints explícitos:** Cada iteración termina esperando confirmación del usuario antes de avanzar.

---

## 2. Pila Tecnológica Base

- **Backend:** Django 5/6 (Python 3.12+)
- **Base de Datos:** SQLite por defecto para desarrollo local (intercambiable por PostgreSQL u otros motores soportados por Django)
- **Frontend:** Django Templates + Tailwind CSS (compilado localmente) + Skill **Impeccable** para diseño y revisión de UI
- **Testing:** Pytest / Pytest-Django o Django TestCase nativo
- **Estándares y Guía Técnica:** [`.agent/django-fullstack.md`](.agent/django-fullstack.md)
- **Contrato de Agentes:** [`.agent/AGENTS.md`](.agent/AGENTS.md)

---

## 3. Estructura del Proyecto

```text
├── .agent/                     # Contratos, estándares y habilidades ODD
│   ├── AGENTS.md               # Contrato y directrices de enrutamiento del agente
│   ├── django-fullstack.md     # Convenciones y estándares Django Fullstack
│   └── skills/                 # Skills para desarrollo asistido
│       ├── backlog/SKILL.md    # Protocolo /backlog
│       ├── story/SKILL.md      # Protocolo /story
│       ├── pair/SKILL.md       # Protocolo /pair
│       └── impeccable/         # Skill de diseño y UI craft
├── core/                       # Configuración raíz de Django (settings, urls, wsgi)
├── manage.py                   # CLI de administración de Django
└── README.md                   # Documentación del starter template
```

---

## 4. Puesta en Marcha

### Prerrequisitos
- Python 3.12+ instalado.
- Entorno virtual activado.

### Primeros Pasos

```bash
# 1. Clonar o inicializar repositorio desde esta plantilla
# 2. Crear y activar el entorno virtual (si aplica)
python3 -m venv .venv
source .venv/bin/activate

# 3. Instalar dependencias del proyecto
pip install django pytest pytest-django

# 4. Ejecutar migraciones base
python manage.py migrate

# 5. Comprobar el estado del sistema
python manage.py check

# 6. Iniciar el servidor local
python manage.py runserver
```

---

## 5. Cómo Iniciar un Nuevo Proyecto con esta Plantilla

1. **Definir el problema:** Pide al agente iniciar con `/backlog` describiendo tu idea general.
2. **Definir el Sistema de Diseño (Paso 0 de Frontend):** El agente inspecciona la estructura y paleta de colores de [https://designeer.xyz](https://designeer.xyz) mediante MCP y genera el archivo `DESIGN.md` en la raíz del proyecto con los tokens y propuesta de layout en Tailwind CSS.
3. **Refinar la primera historia:** Ejecuta `/story` para definir los criterios de aceptación y el mini plan de la historia prioritaria.
4. **Construir paso a paso:** Ejecuta `/pair` para iterar mediante ciclos TDD atómicos (test → rojo → código → verde) con la supervisión directa del desarrollador y la skill `impeccable`.

---

## Créditos

Basado en la metodología y habilidades de [hola-ai](https://github.com/nschurmann/hola-ai) de Nicolás Schürmann (Hola Mundo).
