# Express: URL params

## Qué son los URL params

- Son los datos que ponemos en la url de la petición, pero no los query
- Puede ir con todos los verbos
- Son útiles porque si lo usamos en una petición get, esta la podemos usar desde fetch o desde la url del navegador
- No confundir con los query params

## Url params

- Vídeo
   - Explicar qué son los URL params
   - Mostrar un ejemplo de POST y transformarlo a PUT, usando PostMan
   - Siempre son de tipo texto
   - Ojo cuidado con el orden de los endpoints

## Ejercicios

### Troceando a Rick & Morty

Vamos a crear un API que devuelva los datos de Rick y Morty que ya conocemos pero separados en varios endpoints diferentes

1. Crea un index.js con un servidor
1. Crea un data.json copia dentro los datos de Rick y Morty (https://raw.githubusercontent.com/Adalab/rick-y-morty/master/data/rick-y-morty.json)
1. Haz los siguientes endpoints:
   - Endpoint de tipo GET para recuperar los datos de cada personaje usando la URL `http://localhost:3000/users/1/` y tiene que devolver `{"id": 1,"name": "Rick Sanchez", "status": "Alive" }`
   - Endpoint de tipo GET para recuperar el listado de episodios de un personaje usando la URL `http://localhost:3000/1/episodes` y tiene que devolver
     ```
     [
       "https://rickandmortyapi.com/api/episode/1",
       "https://rickandmortyapi.com/api/episode/2",
       "https://rickandmortyapi.com/api/episode/3",
     ]
     ```
    - Endpoint de tipo GET para recuperar todos los datos de todos los personajes que devuelva los mismos datos de https://raw.githubusercontent.com/Adalab/rick-y-morty/master/data/rick-y-morty.json

Para no tener que montar una web para este ejercicio usa PostMan.