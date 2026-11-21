---
tags: [clase, electiva]
materia: Introducción a la Inteligencia Artificial
fuente: "conocimiento general"
---
# IIA 07 - Aprendizaje, PLN, visión y ética

Materia: [[Introducción a la Inteligencia Artificial]]
Anterior: [[IIA 06 - Razonamiento con incertidumbre y redes bayesianas]]
Siguiente: (fin de la serie)

## Contexto y objetivo
Cierra el curso con las áreas aplicadas actuales: el aprendizaje como forma de construir agentes, el procesamiento de lenguaje natural (PLN), la visión por computador y las implicaciones éticas y sociales. Objetivo: tener una visión panorámica, practicar un clasificador de texto sencillo y reflexionar de forma crítica sobre el impacto de la IA.

## Aprendizaje (panorama)
Un agente que aprende mejora su desempeño con la experiencia. Los tipos (supervisado, no supervisado, por refuerzo) y los algoritmos se desarrollan en [[AA 01 - Fundamentos del aprendizaje automático]]; las redes neuronales en [[RNLD 02 - Perceptrón multicapa y retropropagación]]. Aprendizaje por refuerzo: un agente en un proceso de decisión de Markov (MDP) maximiza la recompensa acumulada descontada $\sum_t\gamma^tr_t$; Q-learning actualiza $Q(s,a)\leftarrow Q(s,a)+\alpha\,[r+\gamma\max_{a'}Q(s',a')-Q(s,a)]$.

## Procesamiento de lenguaje natural
Tareas: clasificación de texto, análisis de sentimiento, traducción, resumen, respuesta a preguntas, reconocimiento de entidades, chatbots.

Representación del texto:
1. **Bolsa de palabras** y **TF-IDF**: $\text{tfidf}(t,d)=\text{tf}(t,d)\cdot\ln\frac{N}{\text{df}(t)}$. Da peso a términos frecuentes en el documento y raros en el corpus.
2. **Incrustaciones (embeddings):** vectores densos (word2vec, GloVe), con la propiedad de que palabras similares quedan cerca (similitud coseno).
3. **Transformadores:** arquitectura basada en autoatención, $\text{Atención}(Q,K,V)=\text{softmax}\!\big(\tfrac{QK^T}{\sqrt{d_k}}\big)V$; base de los modelos de lenguaje grandes (LLM), que predicen el siguiente token y se afinan con instrucciones y retroalimentación humana.

Pipeline clásico: normalizar (minúsculas, quitar signos), tokenizar, eliminar palabras vacías (opcional), vectorizar, clasificar.

## Visión por computador
Tareas: clasificación de imágenes, detección de objetos, segmentación, reconocimiento facial, OCR. Una imagen es una matriz (alto x ancho x canales). **Convolución:** $(I*K)(i,j)=\sum_{u,v}I(i+u,j+v)K(u,v)$; los filtros detectan bordes y texturas. Las **redes convolucionales (CNN)** apilan convolución, no linealidad y submuestreo (pooling) y aprenden los filtros; hoy conviven con transformadores de visión. El aprendizaje por transferencia (reutilizar redes preentrenadas) reduce los datos necesarios.

## Ética e impacto de la IA
- **Sesgo y equidad:** los modelos reproducen sesgos de los datos (selección, histórico, medición); medir el desempeño por subgrupos, definir criterios de equidad (paridad demográfica, igualdad de oportunidades; no siempre compatibles).
- **Transparencia y explicabilidad:** modelos interpretables, importancia de variables, LIME/SHAP.
- **Privacidad:** minimización de datos, anonimización, privacidad diferencial, aprendizaje federado.
- **Responsabilidad y seguridad:** quién responde por un error; robustez ante ataques adversarios; alucinaciones en modelos generativos.
- **Impacto social:** automatización laboral, desinformación y deepfakes, derechos de autor, consumo energético, uso militar.
- **Marcos y normas:** principios de la OCDE, AI Act de la Unión Europea, guías de UNESCO (verificar vigencia actual).
Preguntas guía: ¿a quién beneficia y a quién perjudica?, ¿hay supervisión humana?, ¿se puede apelar una decisión?

## Ejemplo resuelto: TF-IDF y clasificación
Corpus de 4 documentos; el término "oferta" aparece en 1 de ellos.
1. $\text{df}=1$, $N=4$: $\ln(4/1)=1{,}386$.
2. Si "oferta" aparece 3 veces en un documento de 10 palabras, $\text{tf}=0{,}3$: $\text{tfidf}=0{,}416$.
3. El término "de", presente en los 4 documentos: $\ln(4/4)=0$; peso nulo.

Un clasificador (regresión logística o Naive Bayes) sobre estos vectores separa "spam" de "no spam".

## Código
```python
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.pipeline import make_pipeline
from sklearn.model_selection import cross_val_score

textos = [
    "oferta imperdible compra ahora gratis", "gana dinero rápido oferta exclusiva",
    "premio gratis haz clic ahora", "descuento especial solo hoy compra",
    "reunión de proyecto mañana a las 9", "adjunto el informe de la tarea",
    "recordatorio examen de estadística", "nota de la clase de programación",
]
y = [1, 1, 1, 1, 0, 0, 0, 0]          # 1 = spam

modelo = make_pipeline(TfidfVectorizer(lowercase=True),
                       LogisticRegression())
print("CV:", cross_val_score(modelo, textos, y, cv=4).mean())
modelo.fit(textos, y)
print(modelo.predict(["oferta gratis solo hoy", "informe de la reunión"]))

# Convolución 2D a mano (detección de bordes verticales)
import numpy as np
img = np.zeros((6, 6)); img[:, 3:] = 1               # mitad negra, mitad blanca
K = np.array([[-1, 0, 1], [-1, 0, 1], [-1, 0, 1]])   # filtro de Prewitt
out = np.array([[(img[i:i+3, j:j+3] * K).sum() for j in range(4)] for i in range(4)])
print(out)                                            # valores altos en el borde
```

## Errores comunes
- Pensar que más datos eliminan el sesgo (puede amplificarlo si los datos son sesgados).
- Evaluar con un único promedio global y ocultar fallos en subgrupos.
- Fuga de datos en el vectorizador (ajustar TF-IDF antes de dividir): usar `Pipeline`.
- Antropomorfizar los modelos de lenguaje o confiar en sus afirmaciones sin verificar.
- Tratar la ética como un anexo final en lugar de una restricción de diseño.

## Ejercicios propuestos
1. ¿Qué peso TF-IDF tiene un término presente en todos los documentos? *Respuesta: cero.*
2. ¿Por qué el aprendizaje por transferencia ayuda en visión? *Respuesta: las capas iniciales capturan rasgos generales (bordes, texturas) reutilizables, así se necesitan menos datos.*
3. Menciona dos fuentes de sesgo en un sistema de selección de personal. *Respuesta: datos históricos discriminatorios y variables sustitutas (proxies) como código postal.*

## Conexiones
- Probabilidad en clasificación de texto: [[Estadística I]].
- Matrices y convoluciones: [[Matemática III]].
- Modelos para el siguiente paso del curso: [[Aprendizaje Automático]], [[Redes Neuronales y Lógica Difusa]].
- Despliegue de modelos: [[AA 08 - MLOps y despliegue]].

## Fuente
Conocimiento general (Russell y Norvig, caps. 19-28; Jurafsky y Martin, *Speech and Language Processing*; Vaswani et al. 2017). Las normativas citadas deben verificarse en sus textos vigentes. Verificar el temario con el programa oficial.
