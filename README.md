# API de Tareas - Proyecto Django REST Framework

## 📌 Descripción general
Este proyecto corresponde a una **evaluación práctica con Django + DRF**.  
Implementa una API RESTful para la gestión de tareas, cumpliendo los principios REST, versionado y respuestas JSON.

---

## 🚀 Recursos y URIs

| Método | Endpoint | Descripción | Códigos esperados |
|---------|-----------|--------------|-------------------|
| GET | `/api/v1/tareas/` | Lista todas las tareas (paginadas). | 200 OK |
| POST | `/api/v1/tareas/` | Crea una nueva tarea. | 201 Created, 400 Bad Request |
| GET | `/api/v1/tareas/{id}/` | Obtiene el detalle de una tarea por ID. | 200 OK, 404 Not Found |
| PATCH | `/api/v1/tareas/{id}/` | Actualiza parcialmente una tarea (título o hecho). | 200 OK, 400 Bad Request, 404 Not Found |
| DELETE | `/api/v1/tareas/{id}/` | Elimina una tarea. | 204 No Content, 404 Not Found |

---

## 🧱 Modelo principal

**Tarea**
- `id` (AutoField, clave primaria)
- `titulo` (CharField, requerido)
- `hecho` (BooleanField, por defecto `false`)
- `created_at` (DateTimeField, auto_now_add=True)

---

## ⚙️ Códigos HTTP esperados

- **200 OK:** Respuesta exitosa (GET / PATCH)
- **201 Created:** Recurso creado correctamente (POST)
- **204 No Content:** Eliminación exitosa (DELETE)
- **400 Bad Request:** Error de validación en los datos
- **404 Not Found:** ID inexistente o recurso no encontrado

---

## 🧩 Reglas REST explicadas

- **Stateless:**  
  La API no guarda estado del cliente ni usa sesiones; cada solicitud es independiente.

- **JSON:**  
  Todas las peticiones y respuestas usan `Content-Type: application/json`.

- **Versionado:**  
  La API incluye la versión en la ruta (`/api/v1/...`), permitiendo futuras versiones sin romper compatibilidad.

- **Idempotencia:**  
  Los métodos `GET`, `PATCH` y `DELETE` son idempotentes.  
  Ejecutarlos varias veces produce el mismo resultado sin alterar el estado final del recurso.

---

## 🧭 Diagrama de arquitectura

[ Cliente (curl / Postman / SPA) ]
|
HTTP / JSON
|
[ API /api/v1 (ViewSets & URLs - DRF) ]
|
[ Serializers (Validación / Conversión) ]
|
[ Modelos Django (ORM) ]
|
[ Base de datos SQLite (Local) ]


**Descripción de capas:**
- **Cliente:** Envía solicitudes HTTP (por ejemplo con Postman o curl).
- **API / ViewSets:** Define los endpoints REST y controla las operaciones CRUD.
- **Serializers:** Validan y transforman datos entre Python y JSON.
- **Modelos:** Representan las entidades y la lógica de datos.
- **DB:** Almacena la información persistente (SQLite local).

---

## 🛠️ Configuración básica DRF

En `settings.py`:
```python
INSTALLED_APPS = [
    'rest_framework',
    'tareas',
]
