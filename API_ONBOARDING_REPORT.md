# API Onboarding Report

**Laboratorio #3 - Sistemas y Tecnologías Web**
Universidad del Valle de Guatemala | Semestre 1, 2026

---

## Resumen de la API

| Campo        | Detalle                          |
|--------------|----------------------------------|
| Nombre       | RandomDuck                       |
| Base URL     | `https://random-d.uk/api/v2`     |
| Tipo de auth | Ninguna (API pública)            |
| Rate limit   | No documentado oficialmente      |
| Formato      | JSON / image/jpeg / image/gif    |

---

## Tabla de endpoints

| Método | URL | Query Params | Headers | Status Esperado | Status Obtenido |
|--------|-----|--------------|---------|-----------------|-----------------|
| GET | `/list` | — | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/{id}.jpg` | — | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/quack` | — | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/random` | `type=jpg` | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/list` | `limit=10` | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/1.gif` | — | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/http/200` | — | `Accept: application/json` | 200 OK | 200 OK |
| GET | `/99999.jpg` | — | `Accept: application/json` | 404 Not Found | 404 Not Found |
| GET | `/http/400` | — | `Accept: application/json` | 200 OK* | 200 OK |
| GET | `/http/403` | — | `Accept: application/json` | 200 OK* | 200 OK |

> *La API no implementa auth real. Los endpoints `/http/400` y `/http/403` devuelven imágenes de patos representando esos códigos, pero el status HTTP real es 200. Para obtener un 404 real se usó un ID inexistente.

---

## Evidencia de respuestas

###  Exitosa 1 - Listar todos los recursos

**Request:**
```bash
http GET "https://random-d.uk/api/v2/list" Accept:application/json
```

**Response (200 OK):**
```json
{
    "gif_count": 57,
    "image_count": 822,
    "gifs": ["1.gif", "2.gif", "..."],
    "images": ["1.jpg", "2.jpg", "..."],
    "http": ["200.jpg", "400.jpg", "404.jpg", "500.jpg", "..."]
}
```

---

###  Exitosa 2 - Pato random

**Request:**
```bash
http GET "https://random-d.uk/api/v2/random" Accept:application/json
```

**Response (200 OK):**
```json
{
    "message": "Powered by random-d.uk",
    "url": "http://random-d.uk/api/286.jpg"
}
```

---

###  Exitosa 3 - Pato HTTP 200

**Request:**
```bash
http GET "https://random-d.uk/api/v2/http/200" Accept:application/json
```

**Response (200 OK):**
```
Content-Type: image/jpeg
content-disposition: inline; filename=200.jpg
[imagen de pato con texto "200 OK"]
```

---

###  Fallida 1 - 404 ID inexistente

**Request:**
```bash
http GET "https://random-d.uk/api/v2/99999.jpg" Accept:application/json
```

**Response (404 Not Found):**
```
Content-Type: text/html
"404: Not Found - If something should be here, quack very loudly 
and William the IT duck will be with you shortly."
```

---

###  Fallida 2 - 400 Bad Request (simulado)

**Request:**
```bash
http GET "https://random-d.uk/api/v2/http/400" Accept:application/json
```

**Response (200 OK):**
```
Content-Type: image/jpeg
content-disposition: inline; filename=400.jpg
[imagen de pato rojo con texto "400 Bad Request"]
```

> La API devuelve 200 porque el endpoint existe y funciona correctamente. El error 400 está representado visualmente mediante la imagen del pato.
