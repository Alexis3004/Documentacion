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
| nit | Nit del cliente | SI |
| concepto	| Concepto o descripción de la nota | NO |
| tipoNota	| Tipo de nota (1, 2, 3) | SI |
| valorIva	| Valor devuelto del IVA | SI |
| valorTotal	| Valor total de la nota después de impuestos | SI |
| retencion	| Valor en porcentaje devuelto de la retención | SI |
| cedulaUsuario	| Cédula del usuario que lo creo | SI |
| sede	| Sede donde se registró la nota | SI |


### **DETALLE**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| numeroFactura | Número de factura a la que se le aplicó la nota | SI |
| codigoProcedimiento | Código del procedimiento o producto de la nota | SI |
| cantidad | 	Cantidad del procedimiento o producto aplicada en la nota | SI |
| valorProcedimiento	| Valor total devuelto del procedimiento o producto antes de impuestos | SI |
| valorIva	| Valor devuelto del IVA del procedimiento o producto | SI |
| valorTotal	| Valor total devuelto del procedimiento o producto | SI |

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
  "fechaCreacion": "2022-04-07 12:00:00",
  "nit": "1111111111",	
  "concepto": "",
  "tipoNota": "1",
  "valorIva": 0,
  "valorTotal": 10460.10,
  "retencion": "0.16",
  "cedulaUsuario": "999999",
  "sede": "01",
  "detalle": [
    {
      "numeroFactura": "SETP000000000",
      "codigoProcedimiento": "901101",
      "cantidad": 1,
      "valorProcedimiento": 10460.10, 
      "valorIva": 0,
      "valorTotal": 10460.10
    }
  ]
}
```
