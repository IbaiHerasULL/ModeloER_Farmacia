# Modelo Entidad-Relación: Gestión de Farmacia

Este documento describe el modelo entidad-relación (ER) utilizado en el sistema de gestión de farmacia, detallando las entidades y las relaciones que existen entre ellas. 

## Entidades Definidas

### 1. **Medicamento**
   - **Descripción**: Representa los productos farmacéuticos que se venden en la farmacia.
   - **Atributos**:
     - `Código`: Identificador único del medicamento (ejemplo: M001).
     - `Nombre`: Nombre comercial del medicamento (ejemplo: Paracetamol).
     - `Tipo`: Clasificación del medicamento (ejemplo: Analgésico, Antibiótico).
     - `Tipo de Venta`: Indica si es de venta libre o requiere receta (ejemplo: Venta Libre, Bajo Receta).
     - `Precio`: Precio del medicamento en la farmacia (ejemplo: 10.99).
     - `Ud. Stock`: Unidades disponibles en el stock de la farmacia (ejemplo: 100).
     - `Un. Vendidas`: Unidades que han sido vendidas de ese medicamento (ejemplo: 20).

### 2. **Cliente**
   - **Descripción**: Representa a los clientes que compran medicamentos en la farmacia.
   - **Atributos**:
     - `Código`: Identificador único del cliente (ejemplo: C001).
     - `Con Crédito`: Indica si el cliente tiene crédito en la farmacia (ejemplo: Sí/No).

### 3. **Enfermedad**
   - **Descripción**: Representa las enfermedades que pueden ser tratadas con medicamentos.
   - **Atributos**:
     - `Nombre`: Nombre de la enfermedad (ejemplo: Gripe, Migraña).

### 4. **Cuenta Bancaria**
   - **Descripción**: Representa las cuentas bancarias asociadas a los clientes que tienen crédito.
   - **Atributos**:
     - `Número de cuenta`: Número de la cuenta bancaria del cliente (ejemplo: ES7621000000001234567891).
     - `Dinero en la cuenta`: Saldo disponible en la cuenta (ejemplo: 5000.00).

### 5. **Farmacia**
   - **Descripción**: Representa a la farmacia que realiza las ventas de medicamentos.
   - **Atributos**:
     - `Nombre`: Nombre de la farmacia (ejemplo: Farmacia Madrid Centro).

### 6. **Laboratorio**
   - **Descripción**: Representa los laboratorios que fabrican los medicamentos.
   - **Atributos**:
     - `Nombre`: Nombre del laboratorio (ejemplo: Laboratorios Pfizer).
     - `Teléfono`: Número de contacto del cliente (ejemplo: +34 912345678).
     - `Fax`: Número de fax del cliente.
     - `Contacto`: Persona de contacto.
     - `Dirección Postal`: Dirección postal (ejemplo: Calle Mayor, 123, Madrid).
     - `Dirección`: Ubicación física del laboratorio (ejemplo: Calle de la Ciencia, 45, Madrid).

## Relaciones Definidas

### Relaciones Binarias

### 1. **`Enfermedad` *es curada por* `Medicamento` (N:M)**
   - **Descripción**: Una enfermedad puede ser tratada por varios medicamentos, y un medicamento puede ser utilizado para tratar varias enfermedades.
   - **Ejemplo**: La enfermedad "Gripe" puede ser tratada por los medicamentos "Paracetamol" y "Ibuprofeno", y el "Paracetamol" también puede ser usado para tratar la "Fiebre".

### 2. **`Farmacia` *tiene* `Medicamento` (N:M)**
   - **Descripción**: Una farmacia puede tener varios medicamentos en su inventario, y un medicamento puede estar disponible en varias farmacias.
   - **Ejemplo**: La "Farmacia Madrid Centro" tiene los medicamentos "Ibuprofeno" y "Paracetamol", y esos mismos medicamentos también pueden estar disponibles en otras farmacias.

### 3. **`Cliente` *tiene* `Cuenta Bancaria` (1:N)**
   - **Descripción**: Un cliente puede tener varias cuentas bancarias, pero cada cuenta bancaria está asociada a un solo cliente.
   - **Ejemplo**: El cliente "Juan Pérez" puede tener dos cuentas bancarias, una con número "ES7621000000001234567891" y otra con número "ES7621000000009876543210".

### 4. **`Farmacia` *fabrica* `Medicamento` (N:M)**
   - **Descripción**: Una farmacia puede fabricar varios medicamentos, y un medicamento puede ser fabricado por varias farmacias.
   - **Ejemplo**: La "Farmacia Madrid Centro" fabrica los medicamentos "Ibuprofeno" y "Paracetamol", y esos mismos medicamentos pueden ser fabricados por otras farmacias también.
   - 

### Relaciones Ternarias

### 5. **`Cliente` *compra* `Medicamento` *en* `Farmacia` (N:M:P)**
   - **Descripción**: Un cliente puede comprar varios medicamentos en una farmacia, y una farmacia puede vender varios medicamentos a distintos clientes.
   - **Ejemplo**: El cliente "Juan Pérez" compra "Paracetamol" en la "Farmacia Madrid Centro", y otros clientes también pueden comprar "Paracetamol" en esa farmacia.

### 6. **`Farmacia` *compra* `Medicamento` *en* `Laboratorio` (N:M:P)**
   - **Descripción**: Una farmacia puede comprar varios medicamentos, y un medicamento puede ser comprados por varias farmacias en distintos laboratorios.
   - **Ejemplo**: La "Farmacia Madrid Centro" compra el medicamento "Ibuprofeno" en el "Laboratorio Pfizer", y ese mismo medicamento puede ser comprado también en otros laboratorios por otras farmacias.


## Ejemplos ilustrativos del dominio de los atributos

### Atributos de las Entidades
- **Medicamento**
  - `Código`: "M001", "M002", "M003".
  - `Nombre`: "Paracetamol", "Ibuprofeno".
  - `Tipo`: "Analgésico", "Antibiótico".
  - `Tipo de Venta`: "Venta Libre", "Bajo Receta".
  - `Precio`: 10.99, 15.50.
  - `Ud. Stock`: 100, 250.
  - `Un. Vendidas`: 20, 50.

- **Cliente**
  - `Código`: "C001", "C002".
  - `Con Crédito`: "Sí", "No".

- **Enfermedad**
  - `Nombre`: "Gripe", "Migraña".

- **Cuenta Bancaria**
  - `Número de cuenta`: "ES7621000000001234567891", "ES7621000000009876543210".
  - `Dinero en la cuenta`: 5000.00, 3000.50.

- **Farmacia**
  - `Nombre`: "Farmacia Madrid Centro", "Farmacia Sevilla Sur".

- **Laboratorio**
  - `Nombre`: "Laboratorios Pfizer", "Laboratorios Merck".
  - `Teléfono`: "+34 912345678", "+34 912345679".
  - `Fax`: "+34 912345680", "+34 912345681".
  - `Contacto`: "María López", "Pedro García".
  - `Dirección Postal`: "Calle Mayor, 123, Madrid", "Calle de la Ciencia, 45, Madrid".

### Atributos de las Relaciones
- **Enfermedad es curada por Medicamento**
  - Relaciones posibles: 
    - "Gripe" curada por "Paracetamol", "Ibuprofeno".
    - "Migraña" curada por "Ibuprofeno", "Aspirina".

- **Farmacia tiene Medicamento**
  - Relaciones posibles: 
    - "Farmacia Madrid Centro" tiene "Paracetamol", "Ibuprofeno".
    - "Farmacia Sevilla Sur" tiene "Ibuprofeno", "Aspirina".

- **Cliente tiene Cuenta Bancaria**
  - Relaciones posibles:
    - "Juan Pérez" tiene cuentas "ES7621000000001234567891", "ES7621000000009876543210".
    - "Ana García" tiene cuenta "ES7621000000002345678901".

- **Farmacia fabrica Medicamento**
  - Relaciones posibles:
    - "Farmacia Madrid Centro" fabrica "Ibuprofeno", "Paracetamol".
    - "Farmacia Sevilla Sur" fabrica "Aspirina", "Paracetamol".

- **Cliente compra Medicamento en Farmacia**
  - Relaciones posibles:
    - "Juan Pérez" compra "Paracetamol" en "Farmacia Madrid Centro".
    - "Ana García" compra "Ibuprofeno" en "Farmacia Sevilla Sur".

- **Farmacia compra Medicamento en Laboratorio**
  - Relaciones posibles:
    - "Farmacia Madrid Centro" compra "Ibuprofeno" en "Laboratorio Pfizer".
    - "Farmacia Sevilla Sur" compra "Aspirina" en "Laboratorios Merck".


## Restricciones Semánticas

1. **Medicamento con Unidades en Stock y Vendidas:**
   - **Restricción**: El número de unidades vendidas no puede ser mayor al número de unidades en stock.
   - **Implementación (en la base de datos)**: A través de un **trigger** que valide que `Un. Vendidas <= Ud. Stock`.

2. **Relación entre Cliente y Cuenta Bancaria (solo con crédito):**
   - **Restricción**: Un cliente solo puede tener una cuenta bancaria si tiene crédito en la farmacia.
   - **Implementación**: Validación lógica que asegure que el atributo `Con Crédito` sea "Sí" antes de permitir asociar una cuenta bancaria.


