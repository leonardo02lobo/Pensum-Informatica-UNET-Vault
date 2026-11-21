---
tags: [clase, semestre-VII]
materia: Ingeniería Económica
fuente: Material/Tema 2- Factores y Amortización/Parcial 1/ (docx y pdf) y Tema 2- Factores y Amortización/Leonardo Lobo.pdf
---
# Ingeniería Económica - Parcial 1 resuelto

Materia: [[Ingeniería Económica]]
Anterior: [[Ingeniería Económica - Guía de ejercicios Tema 2 resuelta]]
Siguiente: [[Ingeniería Económica - Tema 3 Criterios VA, EA y TIR]]

## Contexto
Evaluación de Ingeniería Económica, lapso 2024-3 (noviembre 2024), UNET, entregada por el estudiante de forma manuscrita (el docx del Parcial 1 contiene 8 imágenes escaneadas; el PDF `Leonardo Lobo.pdf` contiene el enunciado en texto). Se documentan los cuatro enunciados y se resuelven aquí paso a paso con fórmulas (la resolución manuscrita del estudiante no se transcribe; solo se pudo ver legible la primera hoja, donde el capital fijo tangible se suma como 26.200).

## Problema 1: diagrama de flujos
Datos: instalación de máquinas 1.200; seguro de transporte de maquinaria 340; entrenamiento 800; terreno 25.000; inventario de materia prima 345; producto en proceso 270; efectivo en caja 525; materia prima 800; combustible 200; seguros 150; alquileres 300; ingresos brutos 3.200; valor residual 4.000.

**Resolución.**
- Capital fijo tangible: terreno + instalación = 26.200 (coincide con el total que escribe el estudiante en su primera hoja).
- Capital fijo intangible: transporte/seguro 340 + entrenamiento 800 = 1.140 → $CF=27.340$.
- Capital de trabajo: $345+270+525=1.140$.
- $II=CF+CT=28.480$ en $t=0$.
- $C_{op}=800+200+150+300=1.450$ cada año; $IB=3.200$ cada año.
- $VR=4.000$ al final del último año.
Diagrama: flecha hacia abajo de 28.480 en 0; flechas de +3.200 (arriba) y -1.450 (abajo) en 1..n; +4.000 en n.

## Problema 2: tasa efectiva anual
325 crecen a 373 en dos años con interés mensual: $i_{mens}=(373/325)^{1/24}-1=0{,}5756\%$. $i_{ef}=(1{,}005756)^{12}-1=7{,}13\%$ anual (equivale a $\sqrt{373/325}-1$).

## Problema 3: tasa desconocida
$P=800$, $n=7$, $A=125$: $800=125(P/A,i,7)$ → $(P/A,i,7)=6{,}4$. Tanteo: $i=2\%$ → 6,472; $i=2{,}5\%$ → 6,349; interpolando $i\approx2{,}29\%$ por período (dato en las unidades del enunciado: años, es decir 2,29% anual).

## Problema 4: arrendamiento financiero
Juan pagaría 30.000 anuales por 20 años (desde el año 1), más 10.000 en el año 7 y 15.000 en el año 15; tasa 12%. Valor presente:
$$P=30.000(P/A,12\%,20)+10.000(P/F,12\%,7)+15.000(P/F,12\%,15)=224.083+4.523+2.740\approx231.347.$$
Es lo que Juan debería pagar hoy para cancelar el arrendamiento.

## Lecciones
- Separar capital fijo (tangible e intangible), capital de trabajo y flujos de operación.
- Tasa efectiva por raíz enésima, no por división simple.
- Interpolar linealmente entre dos valores tabulados para tasas no tabuladas.

## Errores comunes
Incluir el terreno en depreciación (no se deprecia); tratar capital de trabajo como gasto; olvidar que 2 años = 24 meses al hallar la tasa mensual.

## Ejercicios propuestos
1. Repita P2 con 450 → 520 en 18 meses. (Resp.: 0,81% mensual, 10,2% anual.)
2. P4 con 11% de interés: valor presente. (Resp.: ≈ 251.700.)

## Conexiones
[[Ingeniería Económica - Tema 1 Enfoque sistémico y flujos monetarios]], [[Ingeniería Económica - Tema 2 Interés, tasas y equivalencia]], [[Fórmulas de Matemática Financiera]].

## Fuente
`Parcial 1/Leonardo Lobo V31489733 Ingenieria Economica Parcial 1.docx` y `.pdf` (manuscritos escaneados, 8 págs.) y `Tema 2- Factores y Amortización/Leonardo Lobo.pdf` (enunciados en texto). Verificar con el profesor el tratamiento del seguro de transporte y el entrenamiento como capital fijo intangible.
