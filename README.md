# <h1>**WEB SERVICE**</h1>
- [**SOLICITUD TOKEN**](#token)
- [**ADMISIONES**](#admisiones)

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

## <h2 id="admisiones">**ADMISIONES**</h2>

Estructura de los datos:

### **ENCABEZADO**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| nit | Número de identificación del paciente | SI |
| fecha | Fecha de registro | SI |
| valorTotal	| Valor total del documento | SI |
| valorCopago	| Valor del copago | SI |
| tipoPago	| Tipo de pago del documento | SI |
| usuario	| Usuario quien elaboró el documento | SI |
| cedulaUsuario	| Cédula del usuario quien elaboró el documento | SI |
| cedulaVendedor	| Cédula del vendedor del documento | NO |
| sede	| Sede donde se registró el doc | SI |
| contrato	| Número de contrato | NO |
| poliza	| Número de la poliza registrada | NO |


### **DETALLE**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| codigoProcedimiento | Código del procedimiento o producto | SI |
| valorTotal | Valor total del procedimiento | SI |
| valorIva	| Valor del iva aplicado | SI |
| valorCopago	| Valor del copago | SI |
| valorSinIva	| Valor del procedimiento sin iva | NO |
| cantidad	| Cantidad del procedimiento registrado | SI |
| nivel	| Número de autorización | NO |
| tipoCopago | Tipo de copago | SI |


### **PACIENTE SI NO ESTÁ REGISTRADO**
| CAMPO | DESCRIPCIÓN | REQUERIDO |
| ----- | ---- | --- |
| primerNombre | Primer nombre paciente | SI |
| segundoNombre | Segundo nombre paciente | NO |
| primerApellido	| Primer apellido paciente | SI |
| segundoApellido	| Segundo apellido paciente | NO |
| fechaNacimiento	| Fecha de nacimiento del paciente | SI |
| sexo	| 	Sexo del paciente, valores: M, F, Vacio | NO |
| tipoIdentificacion	| Tipo de identificación (CC, TI, etc) | SI |
| direccion | Dirección del paciente | NO |
| email | 	Email del paciente	 | NO |
| celular | Celular del paciente | NO |
| entidad | Entidad del paciente | SI |
| convenio | Convenio del paciente | NO |
| regimen | Regimen del paciente | SI |
| codigoCiudad | Código de la ciudad | SI |

### Ejemplo de petición para la inserción de admisiones

| Http Headers | Valor |
| ----- | ---- |
| Accept | application/json |
| Authorization | Bearer \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* |

Siendo: \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* el token que obtuvo en la anterior petición.

| TIPO | VALOR |
| ----- | ---- |
| Método: | **POST** |
| URL: | **https://api.manager.clinic/crear/admision** |
| Cuerpo: |  |
```json
{
  "nit": "1111111111",
  "fecha": "2022-04-07 10:00:00",
  "valorTotal": 10460,
  "valorCopago": 500,
  "tipoPago": "001",
  "usuario": "ADMINISTRADOR",
  "cedulaUsuario": "999999",
  "cedulaVendedor": "2222222222",
  "sede": "001",
  "contrato": "",
  "poliza": "",
  "detalle": [
    {
      "codigoProcedimiento": "901101",
      "valorTotal": 10460.10,
      "valorIva": 0,
      "valorCopago": 500.00,
      "valorSinIva": 10460.10,
      "cantidad": 1,
      "nivel": "",
      "tipoCopago": 1
    }
  ],
  "primerNombre": "Pepito",
  "segundoNombre": "",
  "primerApellido": "Pérez",
  "segundoApellido": "",
  "fechaNacimiento": "1998-04-30",
  "sexo": "M",
  "tipoIdentificacion": "CC",
  "direccion": "",
  "email": "",
  "celular": "1234567890",
  "entidad": "900372288",
  "convenio": "",
  "regimen": "1",
  "codigoCiudad": "068001"
}
```

Siendo la primera parte el encabezado, la segunda el detalle y la última parte los datos del paciente por si no se encuentra registrado, de lo contrario no debe enviarse dicha información.
