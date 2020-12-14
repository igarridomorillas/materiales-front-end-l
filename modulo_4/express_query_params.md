# Express: query params

## Qué son los query params

- Son los datos que ponemos en la URL
- A partir del símbolo ?
- Separados por &
- Como va en la url se puede poner en todos endpoints (GET, POST...)
- Tiene mucho sentido usarla con GET
- No confundir con los URL params

## Query params

- Vídeo
   - Explciar qué son los query params
   - Mostrar un ejemplo de GET y transformarlo a POST, usando PostMan
   - Qué pasa si no enviamos un query param, pues que nos retorna undefined

## Ejercicios

### Filtrar / buscar usuarios

Vamos a crear una aplicación de servidor

1. Creamos un data.json con:
   ```json
   [
      { name: 'Sofía' },
      { name: 'María' },
      { name: 'Lucía' },
      { name: 'Julia' },
      { name: 'Tania' }
   ]
   ```
1. Creamos un index.js con su express
1. Importamos el data.json
1. Creamos un endpoint que se llame `api/users`. Este endpoint debe devolver:
   - Si recibe la query param filterByName debe devolver un array con aquellos usuarios coincidentes
   - Si no recibe la query param o está vacía debe devolver todo el array
