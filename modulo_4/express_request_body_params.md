# Express: body params

## Qué son los body params

- Son los datos que ponemos en el cuerpo de la petición
- Puede ir con todos los verbos menos en el GET que no tiene body

## Body params

- Vídeo
   - Explciar qué son los body params
   - Mostrar un ejemplo de POST y transformarlo a PUT, usando PostMan
   - Qué pasa si no enviamos un body param, pues que nos retorna undefined
   - Siempre son de tipo JSON es decir, objeto o array

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

### Calculadora

1. Suma dos números