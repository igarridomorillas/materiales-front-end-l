# Express: header params

## Qué son los header params

- Son los datos que ponemos en la cabecera de la petición
- Puede ir con todos los verbos
- Hay headers por defecto que el navegador y js mete por defecto como:
   - Referer
   - User-Agent
   - Accept, Accept-Encoding, Accept-Language...
- Para qué se suelen usar
- Mostrar un dibujito de cómo se suele hacer un login con un auth

## Headers params en la petición

- Vídeo
   - Explcar qué son los header params
   - Mostrar un ejemplo de GET y transformarlo a POST, usando PostMan
   - Qué pasa si no enviamos un body param, pues que nos retorna undefined
   - Siempre son de tipo texto
   - Siempre son de tipo JSON es decir, objeto o array
   - Case insensitive

## Headers params en la response

- Vídeo
   - Mostrar cómo añado cabeceras a la respuesta `res.header('foo', 123);`.
   - Las cabeceras tienen que ir antes del res.json
   - En el front se recoge así `response.headers.get('foo')`.

## Ejercicios

### Login + Auth (ejercicio pro)

1. Te atreves a hacer el del login + auth