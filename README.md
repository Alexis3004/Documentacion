# <h1>**WEB SERVICE**</h1>

-   [**SOLICITUD TOKEN**](#token)
-   [**FACTURAS**](#facturas)

## <h2 id="token">**SOLICITUD TOKEN**</h2>

Para realizar cualquier petición se debe tener autorización por medio de tokens, por tal motivo se debe solicitar inicialmente el token realizando una petición de tipo POST con un NIT autorizado para hacer peticiones.

### Ejemplo de petición para la obtención del token

| TIPO    | VALOR                                        |
| ------- | -------------------------------------------- |
| Método: | **POST**                                     |
| URL:    | **https://api.manager.clinic/generar/token** |
| Cuerpo: |                                              |

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
    "error": ["El cliente no se encuentra registrado."]
}
```

## <h2 id="facturas">**FACTURAS**</h2>

Estructura de los datos:

### **ENCABEZADO**

| CAMPO               | DESCRIPCIÓN                                    | REQUERIDO                     |
| ------------------- | ---------------------------------------------- | ----------------------------- |
| numeroFactura       | Número de la factura                           | SI                            |
| fechaFactura        | Fecha de la factura                            | SI                            |
| nit                 | Número de identificación del cliente           | SI                            |
| tipoCliente         | Tipo de cliente 1 => entidad, 0 => paciente    | SI CLIENTE NO ESTÁ REGISTRADO |
| formaPago           | Forma de pago de la factura (CONTADO, CREDITO) | SI                            |
| fechaVencimiento    | Fecha de vencimiento de la factura             | SI                            |
| gravada             | Valor de la factura base para iva              | SI                            |
| excluida            | Valor de la factura excluida de iva            | SI                            |
| valorIva            | Valor aplicado de iva                          | SI                            |
| totalFactura        | Total de la factura antes de impuestos         | SI                            |
| saldo               | Total de la factura después de impuestos       | SI                            |
| observacion         | Observación de la factura                      | NO                            |
| centroCosto         | Centro de costo de la factura                  | NO                            |
| prefijo             | Prefijo de la factura                          | SI                            |
| sede                | Sede en donde se registró al factura           | SI                            |
| numeroResolucion    | Número de resolución de la DIAN                | SI                            |
| resolucion          | Leyenda de la resolución                       | NO                            |
| cedulaVendedor      | Cédula del empleado vendedor                   | NO                            |
| porcentajeRetencion | Porcentaje de la retención aplicada            | SI                            |
| totalCopago         | Valor total del copago aplicado                | SI CLIENTE ES UNA ENTIDAD     |
| fechaInicio         | Fecha de inicio del periodo de facturación     | SI CLIENTE ES UNA ENTIDAD     |
| fechaFinal          | Fecha final del periodo de facturación         | SI CLIENTE ES UNA ENTIDAD     |
| evento              | Factura evento (1,0)                           | SI CLIENTE ES UNA ENTIDAD     |
| paquete             | Factura paquete (1,0)                          | NO                            |
| tipoPago            | Código del tipo de pago                        | SI FORMA DE PAGO = 'CONTADO'  |

### **DETALLE**

| CAMPO               | DESCRIPCIÓN                                       | REQUERIDO                 |
| ------------------- | ------------------------------------------------- | ------------------------- |
| codigoProcedimiento | código del procedimiento o producto               | SI                        |
| cantidad            | Cantidad facturada                                | SI                        |
| valorUnitario       | Valor unitario del procedimiento producto         | SI                        |
| gravada             | Valor base para iva                               | SI                        |
| excluida            | Valor excluido de iva                             | SI                        |
| valorIva            | Valor aplicado de iva                             | SI                        |
| valorTotal          | Total del procedimiento antes de aplicar impuesto | SI                        |
| porcentajeIva       | Porcentaje aplicado de iva                        | SI                        |
| fechaAdmision       | Fecha de la admisión                              | NO                        |
| cedulaPaciente      | cédula del paciente                               | SI CLIENTE ES UNA ENTIDAD |
| numeroAutorizacion  | Número de autorización                            | NO                        |
| valorCopago         | Valor del copago aplicado                         | SI CLIENTE ES UNA ENTIDAD |
| tipoCopago          | Tipo de copago registrado                         | SI CLIENTE ES UNA ENTIDAD |
| poliza              | Número de poliza de la atención                   | NO                        |
| contrato            | Número de contrato de la entidad                  | NO                        |
| numeroAdmision      | Número de admisión                                | NO                        |
| prefijoAdmision     | Prefijo de la admisión                            | NO                        |

### **PACIENTE SI NO ESTÁ REGISTRADO**

| CAMPO              | DESCRIPCIÓN                             | REQUERIDO |
| ------------------ | --------------------------------------- | --------- |
| primerNombre       | Primer nombre paciente                  | SI        |
| segundoNombre      | Segundo nombre paciente                 | NO        |
| primerApellido     | Primer apellido paciente                | SI        |
| segundoApellido    | Segundo apellido paciente               | NO        |
| fechaNacimiento    | Fecha de nacimiento del paciente        | SI        |
| sexo               | Sexo del paciente, valores: M, F, Vacio | NO        |
| tipoIdentificacion | Tipo de identificación (CC, TI, etc)    | SI        |
| direccion          | Dirección del paciente                  | NO        |
| email              | Email del paciente                      | NO        |
| celular            | Celular del paciente                    | NO        |
| entidad            | Entidad del paciente                    | NO        |
| convenio           | Convenio del paciente                   | NO        |
| regimen            | Regimen del paciente                    | SI        |
| codigoCiudad       | Código de la ciudad                     | SI        |

### **ENTIDAD SI NO ESTÁ REGISTRADA**

| CAMPO                 | DESCRIPCIÓN                              | REQUERIDO |
| --------------------- | ---------------------------------------- | --------- |
| nombre                | Nombre de la entidad                     | SI        |
| direccion             | Dirección                                | SI        |
| barrio                | Barrio del cliente                       | NO        |
| telefono              | Teléfono                                 | SI        |
| email                 | Celular de la entidad                    | NO        |
| celular               | Email cliente                            | SI        |
| regimen               | Régimen de salud                         | NO        |
| digitoVerificacion    | Dígito de verificación                   | SI        |
| codigoCiudad          | Código de la ciudad                      | SI        |
| tipoPersona           | Tipo de persona (1 jurídica – 2 natural) | NO        |
| responsabilidadFiscal | Responsabilidad fiscal                   | NO        |
| nombreTributo         | Nombre del tributo                       | NO        |

### Ejemplo de petición para la inserción de facturas

| Http Headers  | Valor                                                     |
| ------------- | --------------------------------------------------------- |
| Accept        | application/json                                          |
| Authorization | Bearer \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* |

Siendo: \*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\*.\*\*\*\*\*\*\*\* el token que obtuvo en la anterior petición.

| TIPO    | VALOR                                        |
| ------- | -------------------------------------------- |
| Método: | **POST**                                     |
| URL:    | **https://api.manager.clinic/crear/factura** |

Factura para un paciente

```json
{
    "numeroFactura": "SETT999999990",
    "fechaFactura": "2022-04-20 09:00:00",
    "cedulaVendedor": "",
    "nit": "999999999",
    "formaPago": "CONTADO",
    "fechaVencimiento": "2022-05-30 10:00:00",
    "gravada": 0,
    "excluida": 49500,
    "valorIva": 0,
    "totalFactura": 49500,
    "saldo": 0,
    "fechaInicio": "2022-04-01",
    "fechaFinal": "2022-04-30",
    "totalCopago": 0,
    "prefijo": "SETT",
    "observacion": "",
    "centroCosto": "",
    "evento": "1",
    "paquete": "",
    "sede": "001",
    "porcentajeRetencion": 2,
    "resolucion": "detalle resolución",
    "tipoPago": "001",
    "tipoCliente": 0,
    "detalle": [
        {
            "codigoProcedimiento": "5010101961",
            "cantidad": 1,
            "valorUnitario": 49500.0,
            "gravada": 0,
            "excluida": 49500.0,
            "valorIva": 0,
            "valorTotal": 49500.0,
            "porcentajeIva": 0,
            "numeroAdmision": "",
            "prefijoAdmision": "",
            "fechaAdmision": "",
            "cedulaPaciente": "",
            "valorCopago": 0,
            "numeroAutorizacion": "",
            "contrato": "",
            "poliza": "",
            "tipoCopago": ""
        }
    ],
    "primerNombre": "Paciente",
    "segundoNombre": "",
    "primerApellido": "Prueba2",
    "segundoApellido": "",
    "fechaNacimiento": "1999-04-30",
    "sexo": "",
    "tipoIdentificacion": "CC",
    "direccion": "",
    "email": "",
    "celular": "",
    "entidad": "999999999",
    "convenio": "",
    "regimen": "4",
    "codigoCiudad": "085001"
}
```

Factura para una entidad

```json
{
    "numeroFactura": "SETT999999990",
    "fechaFactura": "2022-04-20 09:00:00",
    "cedulaVendedor": "",
    "nit": "9999999",
    "formaPago": "CREDITO",
    "fechaVencimiento": "2022-05-30 10:00:00",
    "gravada": 0,
    "excluida": 157000,
    "valorIva": 0,
    "totalFactura": 157000,
    "saldo": 0,
    "fechaInicio": "2022-04-01",
    "fechaFinal": "2022-04-30",
    "totalCopago": 50000,
    "prefijo": "SETT",
    "observacion": "",
    "centroCosto": "",
    "evento": "1",
    "paquete": "",
    "sede": "001",
    "porcentajeRetencion": 2,
    "resolucion": "detalle resolución",
    "tipoPago": "001",
    "tipoCliente": 1,
    "detalle": [
        {
            "codigoProcedimiento": "5010101961",
            "cantidad": 1,
            "valorUnitario": 49500.0,
            "gravada": 0,
            "excluida": 49500.0,
            "valorIva": 0,
            "valorTotal": 49500.0,
            "porcentajeIva": 0,
            "numeroAdmision": "",
            "prefijoAdmision": "",
            "fechaAdmision": "",
            "cedulaPaciente": "999999",
            "valorCopago": 50000,
            "numeroAutorizacion": "",
            "contrato": "",
            "poliza": "",
            "tipoCopago": "1"
        }
    ],
    "nombre": "Entidad Prueba2",
    "direccion": "calle 38 #27-105",
    "barrio": "",
    "telefono": "60070085",
    "email": "",
    "celular": "3200000000",
    "regimen": "",
    "digitoVerificacion": "1",
    "codigoCiudad": "068001",
    "tipoPersona": "2",
    "responsabilidadFiscal": "O-13",
    "nombreTributo": "01"
}
```

Siendo para los dos ejemplos, la primera parte el encabezado, la segunda el detalle y la última parte los datos del cliente por si no se encuentra registrado, de lo contrario no debe enviarse dicha información.

Cuando se va a facturar a un cliente que no se encuentra registrado, se debe enviar el tipo de cliente que se debe registrar (0 → Cliente ó 1 → Entidad).
