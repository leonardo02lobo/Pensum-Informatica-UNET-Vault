---
tags: [clase, semestre-V]
materia: Análisis Numérico
fuente: Material/TEMA 2-SOLUCION DE ECUACIONES DE UNA VARIABLE/Teoria/MET NUM ECUACIONES NO LINEALES.pdf
---
# Análisis Numérico - Bisección

Materia: [[Análisis Numérico]]
Anterior: [[Análisis Numérico - Práctica 1 Errores de redondeo]]
Siguiente: [[Análisis Numérico - Newton-Raphson y Secante]]

## Contexto y objetivo
La presentación "Solución de Ecuaciones No Lineales" (Prof. Jenny Pérez) parte del problema de hallar las raíces de $f(x)=0$ cuando no es posible despejar $x$. El método gráfico (ver dónde la curva corta el eje) es poco práctico en casos complejos; se estudian tres métodos iterativos: bisección, Newton-Raphson y secante. Esta nota cubre el primero y el ejemplo guiado de la presentación; el resto está en [[Análisis Numérico - Newton-Raphson y Secante]].

## Fundamento teórico
**Teorema de Bolzano / del valor intermedio.** Si $f$ es continua en $[a,b]$ y $f(a)f(b)<0$, existe $c\in(a,b)$ con $f(c)=0$. El método es **cerrado** (acota la raíz entre dos extremos) y requiere intervalo inicial y función continua. La presentación advierte: en $[a,b]$ puede haber un número **impar** de raíces (el cambio de signo garantiza al menos una, no unicidad).

**Idea.** Se toma el punto medio $x_n=(a_n+b_n)/2$; si $f(a_n)f(x_n)<0$ la raíz está en $[a_n,x_n]$ (se hace $b=x_n$); en otro caso en $[x_n,b_n]$ (se hace $a=x_n$). Cada paso reduce a la mitad la longitud del intervalo.

## Algoritmo (de la presentación)
1. Definir $f$, $[a,b]$ y la tolerancia $\xi$.
2. $i=1$.
3. $x_i=(a_i+b_i)/2$.
4. Si $f(x_i)=0$, terminar. Si no, calcular el error (absoluto o relativo) y comparar con la tolerancia.
5. Si $f(a)f(x_i)<0$, $b=x_i$; si no, $a=x_i$.
6. $i=i+1$ y repetir hasta que error $<\xi$.

## Número de iteraciones a priori
Tras $n$ pasos la longitud es $L/2^n$ ($L=b-a$). Exigiendo $L/2^n\le\varepsilon$:
$$n\ge\frac{\ln L-\ln\varepsilon}{\ln2}=\log_2\frac{L}{\varepsilon}.$$
Por eso "se puede saber de antemano cuántas iteraciones se requieren". Ejemplo: $L=0.2$, $\varepsilon=10^{-6}$: $n\ge\log_2(2\times10^{5})=17.6$, luego $n=18$. Convergencia **lineal** (error $\times\tfrac12$ por iteración): ventaja, siempre converge si se cumplen las hipótesis; desventaja, es lento y no aprovecha la forma de $f$.

## Ejemplo guiado (intersección de $y=\sqrt{x^2+1}$ y $y=\tan x$)
$f(x)=\sqrt{1+x^2}-\tan x$, continua en $(0,\pi/2)$ aunque la tangente no lo sea en todo su dominio. La gráfica muestra cambio de signo en $[0.4,1.4]$ y raíz entre $0.8$ y $1$; se elige $[0.8,1.0]$, con $f(0.8)=0.250986>0$ y $f(1)=-0.143194<0$. Tolerancia $10^{-6}$, máximo 40 iteraciones, criterio $|x_i-x_{i-1}|<\xi$.

Iteración 1: $x_1=0.9$, $f(0.9)=0.085204>0$; como $f(0.8)>0$, $f(a)f(x_1)>0$ y el intervalo pasa a $[0.9,1]$. Iteración 2: $x_2=0.95$, $f(0.95)<0$, intervalo $[0.9,0.95]$; y así hasta la iteración 18, con $x=0.941462$. Comprobación: $\sqrt{0.941462^2+1}=1.3734=\tan(0.941462)$.

## Implementación (función propia)
```matlab
function [r, iter] = biseccion(f, a, b, tol, itmax)
  fa = feval(f, a);
  if fa*feval(f, b) >= 0, error('No hay cambio de signo'); end
  for iter = 1:itmax
    c = (a + b)/2;  fc = feval(f, c);
    if fc == 0 || (b - a)/2 < tol, r = c; return; end
    if fa*fc < 0, b = c; else a = c; fa = fc; end
  end
  r = c;
end
```
La firma `[r,iter]=biseccion(f,a,b,tol,itmax)` es la exigida en [[Análisis Numérico - Práctica 2 Ecuaciones no lineales]].

## Script del material (metodo_biseccion.m)
El material incluye un script mínimo para $f(x)=\sqrt x-\cos x$ en $[0,1]$ con tolerancia $10^{-5}$ y el criterio $(b-a)/2>tol$ en un `while`:
```matlab
f = @(x) sqrt(x) - cos(x);
a = 0; b = 1; tolerance = 1e-5;
while (b - a)/2 > tolerance
    c = (a + b)/2;
    if f(c) == 0, break;
    elseif f(a)*f(c) < 0, b = c; else a = c; end
end
fprintf('La solución aproximada es: %.5f\n', (a+b)/2);
```
Resultado esperado: $x\approx0.6417$ (raíz de $\sqrt x=\cos x$). Pasos necesarios: $\log_2(1/(2\cdot10^{-5}))\approx15.6$, es decir unas 16 iteraciones.

## Errores comunes
- No verificar $f(a)f(b)<0$ (el método "funciona" y devuelve un número sin sentido).
- Intervalos con una **discontinuidad** (p. ej. $\tan x$ o $1/x$): hay cambio de signo sin raíz. Se debe revisar el dominio de continuidad, no solo la gráfica.
- Raíces de multiplicidad par (p. ej. $(x-1)^2$): no hay cambio de signo.
- Usar el residuo $|f(c)|<tol$ como único criterio: con funciones muy planas el residuo es pequeño lejos de la raíz.
- Olvidar `itmax`.

## Ejercicios propuestos
1. Itere a mano 3 veces $f(x)=x^3-x-2$ en $[1,2]$. (Resp.: 1.5, 1.75, 1.625; raíz $1.5214$.)
2. Iteraciones para $10^{-7}$ en $[0,2]$. (Resp.: 25.)
3. Aproxime $\sqrt[3]{25}$ con $x^3-25=0$ en $[2,3]$. (Resp.: 2.9240.)

## Conexiones
Se usa en [[Análisis Numérico - Asignación 1 NACA y ajuste de datos]] y como pregunta teórica de [[Análisis Numérico - Parcial 1 cuestionario resuelto]]. Compare velocidad con [[Análisis Numérico - Newton-Raphson y Secante]].

## Fuente
`Material/TEMA 2-SOLUCION DE ECUACIONES DE UNA VARIABLE/Teoria/MET NUM ECUACIONES NO LINEALES.pdf` y `Scripts Tema 2/Scripts Tema 2/metodo_biseccion.m`.
