<!-- ===================== ENCABEZADO DE LA SEMANA ===================== -->
<p align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:5382A1,50:E76F00,100:B07219&height=160&section=header&text=Semana%202&fontSize=42&fontColor=ffffff&fontAlignY=35&desc=%C3%81lgebra%20de%20Boole%20y%20Formas%20Can%C3%B3nicas&descAlignY=60&descSize=15&animation=fadeIn" width="100%" alt="Encabezado Semana 2">
</p>

<blockquote>
  <p>🎯 <b>Mi Objetivo de Aprendizaje en esta Semana:</b> Durante la segunda semana dimos un salto fundamental: aprendimos un método ordenado y matemático para pasar desde un problema escrito en palabras (enunciado) hasta una tabla de verdad, extraer su expresión algebraica exacta (forma canónica) y finalmente simplificarla para construir un circuito que utilice la menor cantidad posible de chips físicos.</p>
<hr>

<h2>📐 1. Álgebra de Boole: Postulados, Dualidad y Teoremas</h2>
<p>En 1854 George Boole propuso un álgebra para la lógica, y en 1904 Edward Huntington formalizó sus reglas básicas sobre el conjunto {0, 1} con las operaciones + (OR), · (AND) y ' (NOT).</p>

<h3>1.1. Los Postulados de Huntington y el Principio de Dualidad</h3>

<table align="center" width="100%">
  <tr>
    <th>Postulado</th>
    <th>Forma OR (Suma)</th>
    <th>Forma AND (Producto / Dual)</th>
    <th>Explicación intuitiva con interruptores</th>
  </tr>
  <tr>
    <td><b>1. Identidad</b></td>
    <td>X + 0 = X</td>
    <td>X · 1 = X</td>
    <td>Sumar <code>0</code> o multiplicar por <code>1</code> deja la señal intacta.</td>
  </tr>
  <tr>
    <td><b>2. Complemento</b></td>
    <td>X + X' = 1</td>
    <td>X · X' = 0</td>
    <td>Una señal o su opuesta siempre da <code>1</code>; ambas a la vez es imposible (<code>0</code>).</td>
  </tr>
  <tr>
    <td><b>3. Conmutativa</b></td>
    <td>X + Y = Y + X</td>
    <td>X · Y = Y · X</td>
    <td>El orden en que conecto los cables a una compuerta no altera la salida.</td>
  </tr>
  <tr>
    <td><b>4. Distributiva</b></td>
    <td>X(Y + Z) = XY + XZ</td>
    <td><b>X + YZ = (X + Y)(X + Z)</b></td>
    <td>La segunda forma no existe en el álgebra común, pero en Boole es totalmente válida.</td>
  </tr>
</table>

<ul>
  <li><b>¿Qué es el Principio de Dualidad?</b><br>
      Si tenemos cualquier identidad verdadera en el Álgebra de Boole e intercambiamos todos los operadores <b><code>+</code> por <code>·</code></b> (y viceversa) y todos los números <b><code>0</code> por <code>1</code></b> (y viceversa), <b>sin negar ni tocar las variables</b>, obtenemos otra ley booleana igualmente verdadera. Gracias a la dualidad, por cada fórmula que aprendo tengo automáticamente dos.</li>
</ul>

<h3>1.2. Tabla de Consulta de Teoremas para Simplificar</h3>

<table align="center" width="100%">
  <tr>
    <th>Teorema</th>
    <th>Forma OR</th>
    <th>Forma AND (Dual)</th>
    <th>¿Para qué me sirve al simplificar?</th>
  </tr>
  <tr>
    <td><b>Elemento nulo</b></td>
    <td>X + 1 = 1</td>
    <td>X · 0 = 0</td>
    <td>Si una entrada de una OR vale <code>1</code>, toda la expresión se vuelve <code>1</code> (anula el resto).</td>
  </tr>
  <tr>
    <td><b>Idempotencia</b></td>
    <td>X + X = X</td>
    <td>X · X = X</td>
    <td>Me permite eliminar términos repetidos o <b>duplicar un término</b> para factorizarlo con varios vecinos.</td>
  </tr>
  <tr>
    <td><b>Involución</b></td>
    <td>(X')' = X</td>
    <td>(X')' = X</td>
    <td>Dos inversores seguidos en el mismo cable se cancelan entre sí.</td>
  </tr>
  <tr>
    <td><b>Absorción</b></td>
    <td>X + XY = X</td>
    <td>X(X + Y) = X</td>
    <td>Si una variable aparece sola y también multiplicada por otra, el término largo desaparece por completo.</td>
  </tr>
  <tr>
    <td><b>Absorción del complemento</b></td>
    <td>X + X'Y = X + Y</td>
    <td>X(X' + Y) = XY</td>
    <td>Si una variable se suma con su propia negación acompañada de otra (X'Y), la negada X' se elimina.</td>
  </tr>
  <tr>
    <td><b>Adyacencia</b> <i>(Combinación)</i></td>
    <td>XY + XY' = X</td>
    <td>(X+Y)(X+Y') = X</td>
    <td><b>El teorema más usado:</b> si dos términos son idénticos salvo por una variable que cambia de normal a negada, esa variable desaparece.</td>
  </tr>
  <tr>
    <td><b>Consenso</b></td>
    <td>XY + X'Z + YZ = XY + X'Z</td>
    <td>(X+Y)(X'+Z)(Y+Z) = (X+Y)(X'+Z)</td>
    <td>Si aparece X con Y, X' con Z, y además la combinación YZ, el término YZ es redundante y se elimina.</td>
  </tr>
</table>

<h3>1.3. Demostración paso a paso de «La Distributiva que Sorprende»</h3>
<p>En el álgebra del colegio, (A + B)(A + C) nunca es igual a A + BC. Sin embargo, en el Álgebra de Boole sí se cumple. Aquí desarrollo su demostración justificando cada paso:</p>
<ol>
  <li><b>Punto de partida:</b> (A + B)(A + C)</li>
  <li><b>Propiedad distributiva normal:</b> = A · A + A · C + A · B + B · C</li>
  <li><b>Teorema de idempotencia (A · A = A):</b> = A + AC + AB + BC</li>
  <li><b>Factor común A en los tres primeros términos:</b> = A(1 + C + B) + BC</li>
  <li><b>Teorema del elemento nulo (1 + C + B = 1):</b> = A(1) + BC</li>
  <li><b>Postulado de identidad (A · 1 = A):</b> = <b>A + BC</b> ✓</li>
</ol>

<hr>

<h2>🔀 2. Leyes de De Morgan y Resolución de la Práctica en Parejas</h2>
<p>Augustus De Morgan demostró cómo se comporta una negación cuando cubre a todo un producto o a toda una suma:</p>
<ul>
  <li><b>Primera Ley (NAND equivale a OR con entradas negadas):</b> (A · B)' = A' + B'</li>
  <li><b>Segunda Ley (NOR equivale a AND con entradas negadas):</b> (A + B)' = A' · B'</li>
</ul>

<blockquote>
  <p>🧠 <b>Regla mnemotécnica infalible:</b> <b>«Rompe la barra (el paréntesis negado) y cambia el operador»</b>. Donde se parte la negación general, el producto <code>·</code> se transforma en suma <code>+</code> (o la suma <code>+</code> en producto <code>·</code>), y cada pedazo conserva su propio signo de negación.</p>
</blockquote>

<h3>Resolución de la Actividad en Parejas</h3>
<ul>
  <li><b>Ejercicio 1: (A · B · C)'</b><br>
      Rompo el paréntesis negado y cambio productos por sumas: <b>A' + B' + C'</b></li>
  <li><b>Ejercicio 2: (A + B'C)'</b><br>
      Paso 1: A' · (B'C)'<br>
      Paso 2: A' · ((B')' + C')<br>
      Paso 3 (Involución): <b>A'(B + C')</b> (o <b>A'B + A'C'</b>)</li>
  <li><b>Ejercicio 3: (A'B + C)'</b><br>
      Paso 1: (A'B)' · C'<br>
      Paso 2: ((A')' + B') · C' = <b>(A + B')C'</b> (o <b>AC' + B'C'</b>)</li>
</ul>

<hr>

<h2>🧩 3. Minitérminos (mᵢ), Maxitérminos (Mᵢ) y Formas Canónicas (SOP y POS)</h2>
<p>Para convertir cualquier tabla de verdad en una ecuación matemática sin adivinar, disponemos de dos tipos de piezas estándar:</p>
<ol>
  <li><b>Minitérmino (mᵢ):</b> Es un <b>producto (AND)</b> de todas las variables que vale <code>1</code> únicamente en esa fila (si vale <code>1</code> se escribe normal A, si vale <code>0</code> se escribe negada A').</li>
  <li><b>Maxitérmino (Mᵢ):</b> Es una <b>suma (OR)</b> de todas las variables que vale <code>0</code> únicamente en esa fila (si vale <code>0</code> se escribe normal A, si vale <code>1</code> se escribe negada A').</li>
</ol>

<h3>3.1. Tabla de las 8 Piezas Posibles para 3 Variables (A, B, C)</h3>

<table align="center" width="100%">
  <tr>
    <th>Índice i</th>
    <th>Combinación ABC</th>
    <th>Minitérmino mᵢ</th>
    <th>Maxitérmino Mᵢ</th>
    <th>Ejemplo con la Alarma (F: al menos 2 sensores)</th>
  </tr>
  <tr align="center"><td><b>0</b></td><td>0 0 0</td><td>m₀ = A'B'C'</td><td>M₀ = A + B + C</td><td>F = 0 <i>(POS)</i></td></tr>
  <tr align="center"><td><b>1</b></td><td>0 0 1</td><td>m₁ = A'B'C</td><td>M₁ = A + B + C'</td><td>F = 0 <i>(POS)</i></td></tr>
  <tr align="center"><td><b>2</b></td><td>0 1 0</td><td>m₂ = A'BC'</td><td>M₂ = A + B' + C</td><td>F = 0 <i>(POS)</i></td></tr>
  <tr align="center"><td><b>3</b></td><td>0 1 1</td><td>m₃ = A'BC</td><td>M₃ = A + B' + C'</td><td><b>F = 1 <i>(SOP)</i></b></td></tr>
  <tr align="center"><td><b>4</b></td><td>1 0 0</td><td>m₄ = AB'C'</td><td>M₄ = A' + B + C</td><td>F = 0 <i>(POS)</i></td></tr>
  <tr align="center"><td><b>5</b></td><td>1 0 1</td><td>m₅ = AB'C</td><td>M₅ = A' + B + C'</td><td><b>F = 1 <i>(SOP)</i></b></td></tr>
  <tr align="center"><td><b>6</b></td><td>1 1 0</td><td>m₆ = ABC'</td><td>M₆ = A' + B' + C</td><td><b>F = 1 <i>(SOP)</i></b></td></tr>
  <tr align="center"><td><b>7</b></td><td>1 1 1</td><td>m₇ = ABC</td><td>M₇ = A' + B' + C'</td><td><b>F = 1 <i>(SOP)</i></b></td></tr>
</table>

<h3>3.2. Las Dos Formas Canónicas de una Misma Función</h3>
<ul>
  <li><b>SOP Canónica (Suma de Productos):</b> Miro las filas donde <b>F = 1</b> y las uno con <code>+</code>:<br>
      <code>F = Σm(3, 5, 6, 7) = A'BC + AB'C + ABC' + ABC</code></li>
  <li><b>POS Canónica (Producto de Sumas):</b> Miro las filas donde <b>F = 0</b> y las uno con <code>·</code>:<br>
      <code>F = ΠM(0, 1, 2, 4) = (A+B+C)(A+B+C')(A+B'+C)(A'+B+C)</code></li>
</ul>

<hr>

<h2>🚨 4. Caso Guiado: Alarma de 3 Sensores y Ahorro de Hardware</h2>
<p>En una bodega tenemos tres sensores: <b>puerta (A)</b>, <b>ventana (B)</b> y <b>movimiento (C)</b>. La sirena F debe sonar si <b>al menos dos sensores</b> se activan.</p>

<h3>4.1. Simplificación Algebraica de la Alarma</h3>
<p>Partimos de la SOP canónica y aplicamos idempotencia (triplicando ABC) para simplificar:</p>
<ol>
  <li>A'BC + ABC = BC(A' + A) = <b>BC</b></li>
  <li>AB'C + ABC = AC(B' + B) = <b>AC</b></li>
  <li>ABC' + ABC = AB(C' + C) = <b>AB</b></li>
</ol>
<p>Resultado simplificado: <b>F = AB + AC + BC</b></p>

<h3>4.2. Comparación Real de Costo en Circuitos Integrados (CI)</h3>

<table align="center" width="100%">
  <tr>
    <th>Característica</th>
    <th>Versión Canónica (4 términos)</th>
    <th>Versión Simplificada (AB + AC + BC)</th>
  </tr>
  <tr>
    <td><b>Inversores necesarios</b></td>
    <td>3 inversores → <b>1 chip <code>7404</code></b></td>
    <td><b>0 inversores</b></td>
  </tr>
  <tr>
    <td><b>Compuertas AND</b></td>
    <td>4 AND de 3 entradas → <b>2 chips <code>7411</code></b></td>
    <td>3 AND de 2 entradas → <b>1 chip <code>7408</code></b></td>
  </tr>
  <tr>
    <td><b>Compuertas OR</b></td>
    <td>1 OR de 4 entradas → <b>1 chip <code>7432</code></b></td>
    <td>1 OR de 3 entradas → <b>1 chip <code>7432</code></b></td>
  </tr>
  <tr>
    <td><b>Costo Total Físico</b></td>
    <td><b>4 Circuitos Integrados (CI)</b></td>
    <td><b>2 Circuitos Integrados (CI)</b> <i>(¡50 % de ahorro!)</i></td>
  </tr>
</table>

<hr>

<h2>🎫 5. Resolución del Ticket de Salida</h2>
<ol>
  <li><b>Aplique De Morgan a (A' + BC)':</b><br>
      (A')' · (BC)' = <b>A(B' + C')</b> = <b>AB' + AC'</b></li>
  <li><b>Minitérmino m₄ y Maxitérmino M₄ (3 variables):</b><br>
      m₄ = <b>AB'C'</b> · M₄ = <b>A' + B + C</b></li>
</ol>

<hr>

<h2>🛠️ 6. Resolución Completa del Taller Dirigido por Grupos (4 Casos Reales)</h2>

<h3>Caso 1: Luz de Pasillo con Interruptor Maestro</h3>
<ul>
  <li><b>Enunciado:</b> Dos interruptores A y B conmutan la luz; el interruptor maestro M (=1) la apaga siempre.</li>
  <li><b>Tabla resumen:</b> Fila 2 (m₂ = A'BM') y Fila 4 (m₄ = AB'M') activan la luz.</li>
  <li><b>SOP canónica:</b> F = A'BM' + AB'M'</li>
  <li><b>Simplificada:</b> F = M' · (A ⊕ B) (Usa 1 XOR y 1 AND).</li>
</ul>

<h3>Caso 2: Detector de Números Primos de 3 Bits</h3>
<ul>
  <li><b>Enunciado:</b> Entrada de 3 bits ABC (0–7). F = 1 si el número es primo (2, 3, 5, 7).</li>
  <li><b>SOP canónica:</b> F = A'BC' + A'BC + AB'C + ABC</li>
  <li><b>Simplificada:</b> F = A'B + AC (Ahorra un chip completo de compuertas AND).</li>
</ul>

<h3>Caso 3: Control Automático y Manual de Bomba de Agua</h3>
<ul>
  <li><b>Enunciado:</b> Enciende si hay agua en la cisterna (B) y el tanque está bajo (A) o se pide en manual (C).</li>
  <li><b>SOP simplificada:</b> F = AB + C (Equivalente a 1 AND y 1 OR).</li>
</ul>

<h3>Caso 4: Aviso de Cinturón y Puerta en un Vehículo</h3>
<ul>
  <li><b>Enunciado:</b> Suena si el motor está encendido (E) y el cinturón no está puesto (C') o la puerta está abierta (P).</li>
  <li><b>SOP canónica:</b> F = EC'P' + EC'P + ECP</li>
  <li><b>Simplificada:</b> F = EC' + EP = E(C' + P)</li>
</ul>

<hr>

<table align="center" width="100%">
  <tr>
    <td align="left"><a href="Semana_1.md">⬅️ Semana 1</a></td>
    <td align="right"><a href="Semana_3.md">Semana 3 ➡️</a></td>
  </tr>
</table>
