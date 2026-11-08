# Laboratorio TDD — Carrito de compras con JavaScript

Desarrollo Guiado por Pruebas (TDD) con Node.js puro (`node:test` + `node:assert`), sin librerías externas.

## ¿Qué es este laboratorio?

Es una guía práctica para aprender TDD construyendo, prueba por prueba, la lógica de un carrito de compras de una tienda en línea: agregar productos, eliminarlos, aplicar cupones de descuento y calcular el total con IVA.

Se sigue el ciclo **Rojo → Verde → Refactor** en cada iteración:

1. **Rojo**: se escribe una prueba que falle.
2. **Verde**: se escribe el código mínimo para que pase.
3. **Refactor**: se limpia el código con todas las pruebas en verde.

## Requisitos

- Node.js 20 o superior (recomendado 22 LTS)
- Git
- Un editor (VS Code u otro)

No hay dependencias que instalar: el comando de pruebas es `npm test`, que ejecuta `node --test`.

## Estructura del proyecto

```
Laboratorio_TDD/
├── package.json          # configuración y comando de pruebas
├── README.md
├── src/
│   └── carrito.js        # código de producción
└── test/
    └── carrito.test.js   # pruebas (una por iteración/reto)
```

## API del carrito

| Método | Descripción |
|--------|-------------|
| `new Carrito()` | Crea un carrito vacío |
| `agregar(nombre, precio, cantidad = 1)` | Agrega un producto. Valida precio > 0 y cantidad entero positivo. Si el producto ya existe, acumula la cantidad. |
| `eliminar(nombre)` | Quita un producto por nombre. Lanza error si no existe. |
| `actualizarCantidad(nombre, nueva)` | Cambia la cantidad. Si es 0, elimina el producto. Si es negativa, lanza error. |
| `cantidadDeItems()` | Devuelve el total de unidades en el carrito |
| `subtotal()` | Devuelve la suma de precio × cantidad de todos los productos |
| `aplicarCupon(codigo)` | Aplica un cupón válido (`DESC10` = 10 %, `DESC20` = 20 %). Cualquier otro lanza error. |
| `descuento()` | Devuelve el monto descontado (0 si no hay cupón) |
| `baseGravable()` | Devuelve subtotal − descuento |
| `iva()` | Devuelve el IVA (19 %) sobre la base gravable |
| `envio()` | Devuelve $12.000, gratis si la base gravable es 0 o ≥ $150.000 |
| `total()` | Devuelve base gravable + IVA + envío |
| `resumen()` | Devuelve `{ subtotal, descuento, iva, total }` |

## Cómo ejecutar las pruebas

```bash
npm test
```

Resultado esperado con el laboratorio completo:

```
✔ Carrito de compras
ℹ tests 25
ℹ pass 25
ℹ fail 0
```

## Iteraciones del laboratorio

| # | Iteración | Pruebas |
|---|-----------|---------|
| 1 | Carrito vacío | 2 |
| 2 | Agregar productos | 3 |
| 3 | Producto repetido | 1 |
| 4 | Validaciones | 2 |
| 5 | Eliminar productos | 2 |
| 6 | Cupones de descuento | 4 |
| 7 | IVA y total a pagar | 3 |

## Retos adicionales implementados

| Reto | Descripción | Pruebas |
|------|-------------|---------|
| 1 | `resumen()` con subtotal, descuento, IVA y total | 1 |
| 2 | Costo de envío ($12.000, gratis si base ≥ $150.000) incluido en total | 4 |
| 3 | `actualizarCantidad()` (0 elimina, negativo lanza error) | 3 |

**Total: 25 pruebas, 25 pasan, 0 fallan.**

## Valores

Trabajamos en pesos colombianos (COP), sin decimales. Los valores calculados con porcentajes se redondean con `Math.round`.

## Commits

Cada iteración y cada reto adicional tiene su propio commit con mensaje descriptivo (Conventional Commits):

1. `feat: carrito vacío con cantidadDeItems y subtotal en cero (iteración 1)`
2. `feat: agregar productos con cantidad y subtotal (iteración 2)`
3. `feat: producto repetido acumula cantidad en una sola línea (iteración 3)`
4. `feat: validaciones de precio y cantidad en agregar (iteración 4)`
5. `feat: eliminar productos por nombre con error si no existe (iteración 5)`
6. `feat: cupones DESC10 y DESC20 con validación de cupón inválido (iteración 6)`
7. `feat: IVA y total a pagar; refactor extrae baseGravable (iteración 7)`
8. `feat: resumen de la compra con subtotal, descuento, iva y total (reto 1)`
9. `feat: costo de envío (12000, gratis si base >= 150000) incluido en total (reto 2)`
10. `feat: actualizar cantidad (reto 3)`

## Créditos

Taller TDD con JavaScript — Prof. Edwin Rozo Gómez  
Repositorio original: github.com/erozog125/Laboratorio_TDD
