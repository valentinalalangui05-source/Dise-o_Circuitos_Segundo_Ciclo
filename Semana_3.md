# Unidad 1 · Semana 3 — Karnaugh, indiferentes y NAND/NOR

> 🎯 **S1:** expresión mínima SOP y POS (3 y 4 variables) con mapas de Karnaugh, justificando cada grupo.
> 🎯 **S2:** minimizar con indiferentes e implementar solo con NAND, cuantificando el ahorro.

---
## 🅰️ Sesión 1 — Mapas de Karnaugh

**Fundamento:** adyacencia `XY + XY' = X` → si dos minitérminos difieren en una variable, esa variable desaparece.
**Orden Gray `00, 01, 11, 10`:** vecinos cambian 1 solo bit (y la última columna es vecina de la primera).

```
 3 variables                 4 variables
 A \ BC 00 01 11 10          AB \ CD 00 01 11 10
   0     0  1  3  2            00     0  1  3  2
   1     4  5  7  6            01     4  5  7  6
                               11    12 13 15 14
                               10     8  9 11 10
```

**Reglas para agrupar:**
1. Tamaño 2ᵏ (1, 2, 4, 8, 16); un grupo de 2ᵏ elimina *k* variables.
2. Rectangular (sin L ni diagonales).
3. Lo más grande posible.
4. El mapa se enrolla: bordes y esquinas son vecinos.

**Leer un grupo:** constante en 1 → `A` · constante en 0 → `A'` · cambia → desaparece.

**Implicantes:** *implicante* = grupo válido · *primo* = ya no se puede agrandar · *esencial* = único primo que cubre algún 1 (debe estar).
**Solución mínima = primos esenciales + los mínimos necesarios para cubrir el resto** (no siempre es única).

**Ejemplos resueltos**
- `Σm(0,2,4,5,6)` → `F = C' + AB'`
- `Σm(0,1,2,5,8,9,10)`: SOP `B'C' + B'D' + A'C'D` (7 literales) · POS (agrupando 0 y leyendo invertido) `(A'+B')(B'+D)(C'+D')` (6 literales) → gana POS.
- Ticket: `Σm(0,2,5,7,8,10,13,15)` → `B'D' + BD` (= XNOR de B y D).

**Taller (soluciones verificadas)**

| # | Función | Mínimo |
|---|---|---|
| T1 | `Σm(1,3,4,6)` | `A'C + AC'` (= A⊕C) |
| T2 | `Σm(0,1,4,5,6,7,14,15)` | `A'C' + BC` (el primo `A'B` sobra) |
| T3 | `Σm(0,2,5,8,10,13)` | `B'D' + BC'D` |
| T4 | Mapa con errores | (1) columnas en orden binario en vez de Gray; (2) `A'B` redundante; (3) `A'B'C'` contenido en `A'C'`. Correcto: `A'C' + BC` |

---
## 🅱️ Sesión 2 — Indiferentes y NAND/NOR

**Condiciones indiferentes (X):** combinaciones que nunca ocurren (p. ej. BCD usa 10 de 16).
- **Como 1** si agranda un grupo · **como 0** si no ayuda · **nunca sola** (un grupo solo de X es un término inútil).
- Notación: `F = Σm(...) + d(...)`.

**Ejemplo BCD ≥ 5:** `Σm(5,6,7,8,9) + d(10..15)`
- Sin X: `AB'C' + A'BD + A'BC` → 9 literales
- Con X: **`A + BD + BC`** → 5 literales

**Universalidad:** con solo NAND (o solo NOR) se construye todo.

| Función | Solo NAND | Solo NOR |
|---|---|---|
| NOT | `(A·A)'` | `(A+A)'` |
| AND | `((AB)')'` | `(A'+B')'` |
| OR | `(A'·B')'` | `((A+B)')'` |

**SOP mínima → NAND-NAND · POS mínima → NOR-NOR.**

**SOP → NAND-NAND en 4 pasos:**
1. `F = A + BD + BC`
2. `F = ((A + BD + BC)')'` (doble negación)
3. `F = (A' · (BD)' · (BC)')'` (De Morgan)
4. `F = NAND( A', NAND(B,D), NAND(B,C) )`

El literal solo (A) entra **complementado** (NAND usada como inversor). Sigue siendo de dos niveles y de una sola familia.

**Costo en circuitos integrados**

| Versión | Chips | Total |
|---|---|---|
| Sin usar X | 7404 + 7411 + 7432 | 3 CI |
| Con X, AND-OR | 7408 + 7432 | 2 CI |
| Con X, solo NAND | 7400 + 7410 | 2 CI |

*El ahorro vino de las X; la NAND no agrega chips y deja una sola familia.*

**Piensa-pareja-comparte:** `F = A'C' + BC` → `F = NAND( NAND(A',C'), NAND(B,C) )` = 3 NAND2 + 2 inversores (A', C') = 5 NAND2 → **2 chips 7400** (1 si ya hay A' y C').

