# HTTPie Commands - RandomDuck API

## Setup de variables
```bash
export BASE_URL="https://random-d.uk/api/v2"
export ID="5"
export QUERY="quack"
```

---

## 1. Listar todos los recursos disponibles
```bash
http GET "$BASE_URL/list" Accept:application/json
```

---

## 2. Detalle por ID - Pato número 5
```bash
http GET "$BASE_URL/$ID.jpg" Accept:application/json
```

---

## 3. Búsqueda - Pato random con quack
```bash
http GET "$BASE_URL/$QUERY" Accept:application/json
```

---

## 4. Filtro avanzado - Solo formato jpg
```bash
http GET "$BASE_URL/random" Accept:application/json type==jpg
```

---

## 5. Paginación equivalente - Lista con limit
```bash
http GET "$BASE_URL/list" Accept:application/json limit==10
```

---

## 6. Segundo recurso - GIF de pato
```bash
http GET "$BASE_URL/1.gif" Accept:application/json
```

---

## 7. Pato HTTP 200 OK
```bash
http GET "$BASE_URL/http/200" Accept:application/json
```

---

## 8. Error 404 - ID inexistente
```bash
http GET "$BASE_URL/99999.jpg" Accept:application/json
```

---

## 9. Error 400 - Pato Bad Request
```bash
http GET "$BASE_URL/http/400" Accept:application/json
```

---

## 10. Error 403 - Pato Forbidden
```bash
http GET "$BASE_URL/http/403" Accept:application/json
```

---

## 11. Auth correcta simulada

RandomDuck no requiere auth, pero así se vería con token válido:
```bash
export TOKEN="mi_token_real"

http GET "$BASE_URL/random" \
  Accept:application/json \
  Authorization:"Bearer $TOKEN"
```

---

## 12. Auth fallida simulada

Con token inválido, una API con auth respondería 401:
```bash
http GET "$BASE_URL/random" \
  Accept:application/json \
  Authorization:"Bearer token_falso_xyz"
```

> **Nota:** RandomDuck es pública y no requiere auth, ambos comandos devuelven 200. Se incluyen para demostrar la sintaxis correcta de HTTPie con APIs que sí requieren token.
