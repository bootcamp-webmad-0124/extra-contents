# Obtener direcciones y posiciones de lugares

La dependencia [React Google Places Autocomplete](https://www.npmjs.com/package/react-google-places-autocomplete) permite convertir un texto en un objeto con los detalles de una dirección, así como en su posición en términos de latitud y longitud.

## Pasos previos
Pasos previos a la integración de la dependencia:
- Instalar en cliente la dependencia `npm i react-google-places-autocomplete`
- Disponer de un componente sobre el que incluir el campo de texto para escribir la dirección

## Integración

La dependencia ofrece dos métodos:
- `geocodeByAddress` permite obtener los detalles de un lugar a raíz de un string con una dirección
- `getLatLng` permite obtener la latitud y longitud de un lugar a raíz de uno de los objetos retornados por `geocodeByAddress`

Importar en el componente de formulario los métodos:
````javascript
import { geocodeByAddress, getLatLng } from 'react-google-places-autocomplete'
````

Incluir el componente donde se deba mostrar el campo de dirección:
````javascript
 <GooglePlacesAutocomplete
  selectProps={{
    value,
    onChange: getPlaces,
  }}
  apiKey="TU_API_KEY"
/>
````

Contectarlo a un handler:

````javascript
const getPlaces = e => {

  const {value} = e.target

  geocodeByAddress(value)
    .then(results => {
      console.log('Objeto de detalles de la dirección:', results[0])
      getLatLng(results[0])
    })
    .then(coordinates => {
      console.log('Coordenadas de la dirección:', coordinates)
    })
    .catch(error => console.error(error))
}
````
