# LA e-Rubric v2 — Sistema por curso con config.json

## Estructura de archivos por curso

```
tuusuario.github.io/erubric/
│
├── matematicas/
│   ├── index.html       ← copia igual para todos los cursos
│   └── config.json      ← configuras SOLO este archivo por curso
│
├── historia/
│   ├── index.html
│   └── config.json
│
└── biologia/
    ├── index.html
    └── config.json
```

---

## Cómo configurar un nuevo curso

Solo editas `config.json`. El `index.html` es idéntico para todos los cursos.

### Sección `curso`
```json
"curso": {
  "nombre": "Nombre del curso",
  "codigo": "COD-101",
  "docente": "Prof. Apellido",
  "periodo": "2025-I",
  "escala": {
    "tipo": "puntos",   ← "puntos" o "porcentaje"
    "base": 100,        ← solo si tipo es "puntos"
    "aprobacion": 70    ← puntaje mínimo para aprobar
  }
}
```

### Sección `actividades`
Cada actividad tiene estos campos:

| Campo | Valores | Descripción |
|-------|---------|-------------|
| `id` | texto único | Identificador (ej. "a1", "tarea1") |
| `nombre` | texto | Nombre visible de la actividad |
| `tipo` | `"sumativa"` / `"formativa"` | Las sumativas suman al puntaje final, las formativas no |
| `peso` | número 0–100 | % del peso en el puntaje final (solo afecta a sumativas) |
| `escala.tipo` | `"puntos"` / `"porcentaje"` | Escala de calificación de esta actividad |
| `escala.base` | número | Base de puntos (ej. 10, 20) — solo si tipo es "puntos" |

### Tipos de enrichment por criterio
| Valor | Descripción |
|-------|-------------|
| `"none"` | Sin analytics — criterio simple |
| `"collab"` | Colaboración (nº de posts/foro) |
| `"grade"` | Calificaciones previas (%) |
| `"study"` | Acceso a materiales (nº de accesos) |

---

## Los pesos sumativos deben sumar 100%

```json
{ "nombre": "Tarea 1", "tipo": "sumativa", "peso": 15 }  ← 15%
{ "nombre": "Parcial",  "tipo": "sumativa", "peso": 35 }  ← 35%
{ "nombre": "Final",    "tipo": "sumativa", "peso": 50 }  ← 50%
                                                    TOTAL: 100% ✓
```

Las formativas tienen `"peso": 0` — no afectan al cálculo.

---

## Cómo embeber en Moodle

En el editor HTML de cualquier actividad o etiqueta:

```html
<iframe
  src="https://TU-USUARIO.github.io/erubric/matematicas/"
  width="100%"
  height="800"
  frameborder="0"
  style="border-radius:8px;border:1px solid #e2e0d8;">
</iframe>
```

Cambia `matematicas/` por la carpeta de cada curso.

---

## Para actualizar criterios o agregar actividades

1. Edita `config.json` en GitHub (lápiz ✏️)
2. Haz commit
3. En 30 segundos el cambio está publicado — sin tocar `index.html`
