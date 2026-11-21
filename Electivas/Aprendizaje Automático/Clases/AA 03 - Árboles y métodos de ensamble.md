---
tags: [clase, electiva]
materia: Aprendizaje Automático
fuente: "conocimiento general; ruta leída: /home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/07 - AutoGluon.md"
---
# AA 03 - Árboles y métodos de ensamble

Materia: [[Aprendizaje Automático]]
Anterior: [[AA 02 - Regresión lineal y logística]]
Siguiente: [[AA 04 - SVM, k-NN y Naive Bayes]]

## Contexto y objetivo
Los árboles de decisión particionan el espacio de variables con reglas simples y son la base de los métodos más exitosos en datos tabulares (bosques aleatorios, gradient boosting). Objetivo: construir un árbol calculando impureza y ganancia, y entender por qué los ensambles reducen sesgo o varianza.

## Árbol de decisión (CART)
En cada nodo se elige la variable $j$ y el umbral $t$ que mejor reducen la impureza al dividir en izquierdo ($L$) y derecho ($R$).

Impureza de un nodo con proporciones de clase $p_k$:
- **Gini:** $G=1-\sum_kp_k^2$.
- **Entropía:** $H=-\sum_kp_k\log_2p_k$.
- Regresión: varianza (ECM) de $y$ en el nodo.

Ganancia: $\Delta=I(\text{padre})-\frac{N_L}{N}I(L)-\frac{N_R}{N}I(R)$.

Se divide recursivamente hasta un criterio de parada (profundidad máxima, mínimo de muestras por hoja) o se poda (poda por coste-complejidad, `ccp_alpha`). Un árbol sin límite memoriza los datos (varianza alta). Ventajas: interpretable, no requiere escalar, maneja no linealidades e interacciones. Desventajas: inestable, fronteras ortogonales.

## Ensambles
**Bagging (agregación bootstrap):** entrenar $B$ modelos sobre muestras bootstrap (con reemplazo) y promediar/votar. Reduce varianza.

**Bosque aleatorio (Random Forest):** bagging de árboles profundos más un submuestreo aleatorio de $m\approx\sqrt d$ variables en cada división, que decorrelaciona árboles. Estimación gratuita del error con las muestras fuera de la bolsa (OOB, ~37 % por árbol). Importancia de variables por reducción media de impureza o por permutación.

**Boosting:** modelos débiles en secuencia, cada uno corrige a los anteriores. Reduce sesgo.
- AdaBoost: reponderar muestras mal clasificadas.
- **Gradient Boosting:** $F_m(x)=F_{m-1}(x)+\nu\,h_m(x)$, donde $h_m$ ajusta los residuos (el gradiente negativo de la pérdida): $r_i=-\partial\ell(y_i,F)/\partial F$. Con pérdida cuadrática, $r_i=y_i-F_{m-1}(x_i)$. Implementaciones modernas: XGBoost, LightGBM, CatBoost. Hiperparámetros clave: `learning_rate` $\nu$, número de árboles, `max_depth`, submuestreo.

**Stacking:** un metamodelo combina las predicciones de modelos base (usando predicciones fuera de muestra). AutoGluon apila y empaqueta modelos en capas; ver [[07 - AutoGluon]] y la comparativa [[09 - Comparativa frameworks AutoML]].

## Ejemplo resuelto: ganancia de Gini
Nodo con 10 muestras: 6 de clase A y 4 de B. División por $x\le5$: izquierda 5 muestras (4 A, 1 B), derecha 5 (2 A, 3 B).
1. Padre: $G=1-0{,}6^2-0{,}4^2=0{,}48$.
2. Izquierda: $G_L=1-0{,}8^2-0{,}2^2=0{,}32$.
3. Derecha: $G_R=1-0{,}4^2-0{,}6^2=0{,}48$.
4. Ponderado: $0{,}5\cdot0{,}32+0{,}5\cdot0{,}48=0{,}40$.
5. Ganancia: $0{,}48-0{,}40=0{,}08$. Se compara con otras divisiones y se elige la mayor.

Boosting cuadrático con dos pasos: $y=(3,5,9)$, $F_0=\bar y=5{,}667$. Residuos: $(-2{,}667;-0{,}667;3{,}333)$. Si $h_1$ los ajusta perfectamente y $\nu=0{,}5$: $F_1=5{,}667+0{,}5\cdot$residuo $=(4{,}33;5{,}33;7{,}33)$, más cerca del objetivo.

## Código
```python
from sklearn.datasets import load_breast_cancer
from sklearn.model_selection import cross_val_score, train_test_split
from sklearn.tree import DecisionTreeClassifier, export_text
from sklearn.ensemble import RandomForestClassifier, GradientBoostingClassifier

X, y = load_breast_cancer(return_X_y=True)
names = load_breast_cancer().feature_names

arbol = DecisionTreeClassifier(max_depth=3, criterion="gini", random_state=0)
arbol.fit(X, y)
print(export_text(arbol, feature_names=list(names)))   # reglas legibles

modelos = {
    "árbol profundo": DecisionTreeClassifier(random_state=0),
    "bosque": RandomForestClassifier(300, oob_score=True, random_state=0),
    "boosting": GradientBoostingClassifier(learning_rate=0.1, n_estimators=200,
                                           max_depth=3, random_state=0),
}
for n, m in modelos.items():
    print(n, cross_val_score(m, X, y, cv=5).mean().round(3))

rf = modelos["bosque"].fit(X, y)
print("OOB:", rf.oob_score_.round(3))
imp = sorted(zip(rf.feature_importances_, names), reverse=True)[:5]
print(imp)
```

## Errores comunes
- No limitar la profundidad de un árbol único.
- Creer que la importancia por impureza es fiable con variables de alta cardinalidad (sesga a favor); preferir permutación.
- Boosting con tasa de aprendizaje alta y muchos árboles (sobreajuste); usar parada temprana.
- Aplicar bootstrap sin tener en cuenta datos agrupados o temporales.
- Codificar categorías como enteros arbitrarios para modelos que no los soportan (ver [[AA 07 - Preprocesamiento e hiperparámetros]]).

## Ejercicios propuestos
1. Calcula Gini de un nodo 50/50. *Respuesta: $0{,}5$.*
2. ¿Qué reduce el bagging, sesgo o varianza? *Respuesta: varianza.*
3. ¿Qué porcentaje aproximado de muestras queda fuera de cada bootstrap? *Respuesta: $\approx36{,}8\,\%$ ($e^{-1}$).*

## Conexiones
- Entropía e información: [[Estadística I]] y [[Matemática Discreta]].
- Estructuras de árbol: [[Estructura de Datos]].
- Ensambles automáticos en la práctica: [[07 - AutoGluon]], [[05 - auto-sklearn]].

## Fuente
Conocimiento general (Breiman 1984, 2001; Friedman 2001; *ESL* caps. 9-10, 15). Material del vault leído: `/home/leonardo/Documentos/Obsidian Vault/Aprendizaje automatico/07 - AutoGluon.md`. Verificar el temario con el programa oficial.
