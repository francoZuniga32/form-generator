# form-generator

Generador simple de formularios boostrap. puede generar sus formularios de forma [Online](https://francozuniga32.github.io/form-generator/), o de forma local clonando y siguiendo etos pasos:

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

# Form Generator

- Agregar filas / Eliminar filas

- Agregar Inputs
    
    |     |     |
    | --- | --- |
    | Inputs | Características |
    | Text |     |
    | Number |     |
    | Checkbox |     |
    | Switch |     |
    | Password |     |
    | Range | Valor Minino, Valor Máximo, Cantidad por pasos |
    | Select | Agregar los opciones, eliminar |
    | Archivo |     |
    | Color |     |
    | Date |     |
    | Time |     |
    

## Funcionalidades futuras

- [x]  Edición de cantidad de columnas para las filas 
- [x]  Eliminar los inputs de las filas 
- [x]  Editar el tamaño para los dispositivos (sm, md, lg) 
- [ ]  Funciones extras de Inputs

|     |     |
| --- | --- |
| Inputs | Características |
| Number | Valor Minino, Valor Máximo, Aceptar double |
| Archivo | Tipo de Archivos Aceptados |
| Date | Fecha Minino, Fecha Máximo | 
- [ ]  Date TIme Select 
- [ ]  Un nuevo Date Input 

## Bugs

|     |     |     |
| --- | --- | --- |
| Bug | Descripcion | Estado |
| Select luego de cargar | no se reinicia el select | Resuelto |
| Chenckbox | no muestra correctamente el contenido | Detectado |
| valores menores a sm | row-cols-sm-1 no funciona para valores menores a 576 | Detectado |