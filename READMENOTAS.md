# <h1>**WEB SERVICE**</h1>
- [**SOLICITUD TOKEN**](#token)
- [**NOTAS CRÉDITO**](#notas)

## <h2 id="token">**SOLICITUD TOKEN**</h2> 

Para realizar cualquier petición se debe tener autorización por medio de tokens, por tal motivo se debe solicitar inicialmente el token realizando una petición de tipo POST con un NIT autorizado para hacer peticiones.

### Ejemplo de petición para la obtención del token

| TIPO | VALOR |
| ----- | ---- |
| Método: | **POST** |
| URL: | **https://api.manager.clinic/generar/token** |
| Cuerpo: |  |
```json
{
    "nit": "3333333333"
}
```

Si el NIT tiene autorización recibirá una respuesta de la siguiente manera:

```json
{
  "Token": "********.********.********"
}
```

De lo contrario recibirá la siguiente respuesta

```json
{
  "error": [
    "El cliente no se encuentra registrado."
  ]
}
```

## <h2 id="notas">**NOTAS CRÉDITO**</h2>

Estructura de los datos:

### **ENCABEZADO**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| fechaCreacion | Fecha de creación | SI |
| concepto	| Concepto o descripción de la nota | NO |
| tipoNota	| Tipo de nota (1, 2, 3) | SI |
| valorIva	| Valor devuelto del IVA | SI |
| valorTotal	| Valor total de la nota después de impuestos | SI |
| retencion	| Valor en porcentaje devuelto de la retención | SI |
| cedulaUsuario	| Cédula del usuario que crea la nota | SI |
| sede	| Sede donde se registró la nota | SI |
| numeroFactura | Número de factura a la que se le aplicó la nota | SI |


### **DETALLE**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| articulo | Código del procedimiento o producto de la nota | SI |
| cantidad | 	Cantidad del procedimiento o producto aplicada en la nota | SI |
| valorArticulo	| valor unitario devuelto del procedimiento o producto antes de impuestos | SI |
| valorIva	| Valor devuelto del IVA del procedimiento o producto | SI |
| valorTotal	| Valor total devuelto del procedimiento o producto antes de impuestos | SI |

### Ejemplo de petición para la inserción de notas crédito

| Http Headers | Valor |
| ----- | ---- |
| Accept | application/json |
| Authorization | Bearer \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* |

Siendo: \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* el token que obtuvo.

| TIPO | VALOR |
| ----- | ---- |
| Método: | **POST** |
| URL: | **https://api.manager.clinic/crear/nota/credito** |
| Cuerpo: |  |
```json
{
  "fechaCreacion": "2022-06-23 08:25:00",
  "concepto": "Dev. Total Factura",
  "tipoNota": "1",
  "valorIva": 275.50,
  "valorTotal": 5583.5,
  "retencion": 142,
  "cedulaUsuario": "999999",
  "sede": "01",
  "numeroFactura": "SETP000000000",
  "detalle": [
      {
        "articulo": "00100001",
        "cantidad": 1,
        "valorArticulo": 1450,
        "valorIva": 275.50,
        "porcentajeIva": 19,
        "valorTotal": 1450
    },
    {
        "articulo": "00100005",
        "cantidad": 1,
        "valorArticulo": 4000,
        "valorIva": 0,
        "porcentajeIva": 0,
        "valorTotal": 4000
    }
  ]
}
```
