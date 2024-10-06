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

### 1. **`Medicamento` *cura* `Enfermedad` (1:N)**
   - **Descripción**: Un medicamento puede estar indicado para curar una o varias enfermedades.
   - **Ejemplo**: El medicamento "Paracetamol" puede curar las enfermedades "Gripe" y "Fiebre".

### 2. **`Medicamento` *es fabricado por* `Laboratorio` (N:1)**
   - **Descripción**: Cada medicamento es fabricado por un único laboratorio, pero un laboratorio puede fabricar varios medicamentos.
   - **Ejemplo**: "Laboratorios Pfizer" fabrica el medicamento "Ibuprofeno".

### 3. **`Cliente` *realiza* `Compra` (1:N)**
   - **Descripción**: Un cliente puede realizar varias compras, pero cada compra es realizada por un solo cliente.
   - **Ejemplo**: El cliente "Juan Pérez" realiza una compra de "Paracetamol" y "Ibuprofeno".

### 4. **`Compra` *incluye* `Medicamento` (N:M)**
   - **Descripción**: Una compra puede incluir varios medicamentos y un medicamento puede estar presente en varias compras.
   - **Ejemplo**: En una compra, se puede adquirir tanto "Ibuprofeno" como "Paracetamol".

### 5. **`Cliente` *tiene* `Cuenta Bancaria` (1:1)**
   - **Descripción**: Un cliente solo puede tener una cuenta bancaria si tiene crédito disponible en la farmacia.
   - **Ejemplo**: El cliente "Juan Pérez" tiene la cuenta bancaria con número "ES7621000000001234567891" porque tiene crédito.

### 6. **`Farmacia` *tiene relación con* `Laboratorio` (1:N)**
   - **Descripción**: Una farmacia puede trabajar con varios laboratorios, pero un laboratorio puede trabajar con una sola farmacia.
   - **Ejemplo**: La farmacia "Farmacia Madrid Centro" tiene relación con los laboratorios "Pfizer" y "Roche".

## Ejemplos ilustrativos del dominio de los atributos



## Restricciones Semánticas

1. **Medicamento con Unidades en Stock y Vendidas:**
   - **Restricción**: El número de unidades vendidas no puede ser mayor al número de unidades en stock.
   - **Implementación (en la base de datos)**: A través de un **trigger** que valide que `Un. Vendidas <= Ud. Stock`.

2. **Relación entre Cliente y Cuenta Bancaria (solo con crédito):**
   - **Restricción**: Un cliente solo puede tener una cuenta bancaria si tiene crédito en la farmacia.
   - **Implementación**: Validación lógica que asegure que el atributo `Con Crédito` sea "Sí" antes de permitir asociar una cuenta bancaria.


