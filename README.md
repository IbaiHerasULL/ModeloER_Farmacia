# Modelo Entidad-Relación: Gestión de Farmacia

Este documento describe el modelo entidad-relación (ER) utilizado en el sistema de gestión de farmacia, detallando las entidades y las relaciones que existen entre ellas.

## Entidades Definidas

### 1. Medicamento
Descripción: Representa los productos farmacéuticos que se venden en la farmacia.
- **Atributos:**
  - `Código`: Identificador único del medicamento (ejemplo: M001).
  - `Nombre`: Nombre comercial del medicamento (ejemplo: Paracetamol).
  - `Tipo`: Clasificación del medicamento (ejemplo: Analgésico, Antibiótico).
  - `Tipo de Venta`: Indica si es de venta libre o requiere receta (ejemplo: Venta Libre, Bajo Receta).
  - `Precio`: Precio del medicamento en la farmacia (ejemplo: 10.99).

### 2. Cliente
Descripción: Representa a los clientes que compran medicamentos en la farmacia.
- **Atributos:**
  - `Código`: Identificador único del cliente (ejemplo: C001).
  - `Con Crédito`: Indica si el cliente tiene crédito en la farmacia (ejemplo: Sí/No).

### 3. Enfermedad
Descripción: Representa las enfermedades que pueden ser tratadas con medicamentos.
- **Atributos:**
  - `Nombre`: Nombre de la enfermedad (ejemplo: Gripe, Migraña).

### 4. Cuenta Bancaria
Descripción: Representa las cuentas bancarias asociadas a los clientes que tienen crédito.
- **Atributos:**
  - `Número de cuenta`: Número de la cuenta bancaria del cliente (ejemplo: ES7621000000001234567891).
  - `Dinero en la cuenta`: Saldo disponible en la cuenta (ejemplo: 5000.00).

### 5. Farmacia
Descripción: Representa a la farmacia que realiza las ventas de medicamentos.
- **Atributos:**
  - `Nombre`: Nombre de la farmacia (ejemplo: Farmacia Madrid Centro).

### 6. Laboratorio
Descripción: Representa los laboratorios que fabrican los medicamentos.
- **Atributos:**
  - `Nombre`: Nombre del laboratorio (ejemplo: Laboratorios Pfizer).
  - `Teléfono`: Número de contacto del laboratorio (ejemplo: +34 912345678).
  - `Fax`: Número de fax del laboratorio.
  - `Contacto`: Persona de contacto.
  - `Dirección Postal`: Dirección postal (ejemplo: Calle Mayor, 123, Madrid).

## Relaciones Definidas

### Relaciones Binarias

1. **`Enfermedad` *es curada por* `Medicamento` (N:M)**
   - Descripción: Una enfermedad puede ser tratada por varios medicamentos, y un medicamento puede ser utilizado para tratar varias enfermedades.
   - Ejemplo: La enfermedad "Gripe" puede ser tratada por los medicamentos "Paracetamol" y "Ibuprofeno".

2. **`Farmacia` *tiene* `Medicamento` (N:M)**
   - Descripción: Una farmacia puede tener varios medicamentos en su inventario, y un medicamento puede estar disponible en varias farmacias.
   - Atributos adicionales:
     - `Precio`: Precio del medicamento en la farmacia (ejemplo: 10.99, 15.50).
     - `Ud. Stock`: Unidades disponibles en el stock de la farmacia (ejemplo: 100, 250).
     - `Un. Vendidas`: Unidades que han sido vendidas de ese medicamento (ejemplo: 20, 50).
   - Ejemplo: La "Farmacia Madrid Centro" tiene "Ibuprofeno" a un precio de 10.99 con `Ud. Stock` de 100 y `Un. Vendidas` de 20, mientras que "Farmacia Sevilla Sur" tiene "Ibuprofeno" a 15.50 con `Ud. Stock` de 250 y `Un. Vendidas` de 50.

3. **`Cliente` *tiene* `Cuenta Bancaria` (1:N)**
   - Descripción: Un cliente puede tener varias cuentas bancarias, pero cada cuenta bancaria está asociada a un solo cliente.
   - Ejemplo: "Juan Pérez" tiene cuentas "ES7621000000001234567891", "ES7621000000009876543210".

4. **`Farmacia` *fabrica* `Medicamento` (N:M)**
   - Descripción: Una farmacia puede fabricar varios medicamentos, y un medicamento puede ser fabricado por varias farmacias.
   - Ejemplo: La "Farmacia Madrid Centro" fabrica "Ibuprofeno" y "Paracetamol", mientras que "Farmacia Sevilla Sur" fabrica "Aspirina" y "Paracetamol".

### Relaciones Ternarias

5. **`Cliente` *compra* `Medicamento` *en* `Farmacia` (N:M:P)**
   - Descripción: Un cliente puede comprar varios medicamentos en una farmacia, y una farmacia puede vender varios medicamentos a distintos clientes.
   - Atributos adicionales:
     - `Fecha`: Fecha de la compra (ejemplo: 2024-10-06).
     - `Unidades Compradas`: Cantidad de unidades compradas (ejemplo: 2).
   - Ejemplo: "Juan Pérez" compra "Paracetamol" en "Farmacia Madrid Centro" el "2024-10-06", adquiriendo "2" unidades.

6. **`Farmacia` *compra* `Medicamento` *en* `Laboratorio` (N:M:P)**
   - Descripción: Una farmacia puede comprar varios medicamentos, y un medicamento puede ser comprado por varias farmacias en distintos laboratorios.
   - Ejemplo: "Farmacia Madrid Centro" compra "Ibuprofeno" en "Laboratorio Pfizer".

## Ejemplos Ilustrativos del Dominio de los Atributos

- **Medicamento**
  - `Código`: M001
  - `Nombre`: Paracetamol
  - `Tipo`: Analgésico
  - `Tipo de Venta`: Venta Libre
  - `Precio`: 10.99

- **Cliente**
  - `Código`: C001
  - `Con Crédito`: Sí

- **Enfermedad**
  - `Nombre`: Gripe

- **Cuenta Bancaria**
  - `Número de cuenta`: ES7621000000001234567891
  - `Dinero en la cuenta`: 5000.00

- **Farmacia**
  - `Nombre`: Farmacia Madrid Centro

- **Laboratorio**
  - `Nombre`: Laboratorios Pfizer
  - `Teléfono`: +34 912345678
  - `Fax`: 912345679
  - `Contacto`: Juan López
  - `Dirección Postal`: Calle Mayor, 123, Madrid

## Restricciones Semánticas

### Medicamento con Unidades en Stock y Vendidas
- **Restricción**: El número de unidades vendidas no puede ser mayor al número de unidades en stock.
- **Implementación**: A través de un trigger que valide que `Un. Vendidas <= Ud. Stock`.

### Relación entre Cliente y Cuenta Bancaria (solo con crédito)
- **Restricción**: Un cliente solo puede tener una cuenta bancaria si tiene crédito en la farmacia.
- **Implementación**: Validación lógica que asegure que el atributo `Con Crédito` sea "Sí" antes de permitir asociar una cuenta bancaria.
