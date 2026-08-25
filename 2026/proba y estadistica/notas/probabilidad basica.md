condicionalidad e independencia:
la probabilidad de ocurrencia del evento A puede depender de la ocurrencia de otro evento B. si esa dependencia existe, a la probabilidad asociada de le llama probabilidad condicional. se represnta por P(A/B) y se interpreta como probabilidad de A dado B.

definicion probabilidad condicional:
𝑷 (𝑨 / 𝑩)= 𝑷(𝑨 ∩ 𝑩) / 𝑷(𝑩)

es una generalizacion de la probabilidad de un evento, en donde implicitamente se ha considerado la ocurrencia del evento seguro

esta probabilidad condicional, es generalizcion de la probabilidad de evento, en donde implicitamente se considera la ocurrencia del evento seguro

### regla de multiplicacion
𝑷 (𝑨 ∩ 𝑩) = 𝑷 (𝑨) . 𝑷(𝑩/𝑨)

%%>por que divide por esa interseccion? %%

dados 3 eventos: A, B y C, definimos:
𝑷(𝑨 ∩ 𝑩 ∩ 𝑪)= 𝑷(𝑨) .𝑷(𝑩⁄𝑨).𝑷(𝑪/𝑨 ∩ 𝑩)

### independencia de eventos
dos eventos A y B son independientes cuando la ocurrencia de uno no afecta a la ocurrencia del otro, en terminos de probabilidades

𝑷(𝑨⁄𝑩) = 𝑷(𝑨) 
𝑷(𝑩⁄𝑨) = 𝑷(𝑩)

entonces la regla de multiplicacion resulta que si A y B son independientes: 
𝑷(𝑨 ∩ 𝑩)= 𝑷(𝑨). 𝑷(𝑩)

- ojo: dos eventos mutuamente excluyentes y no vacios (P(A)>0, P(B)>0) NO pueden ser independientes: P(A∩B)=0 ≠ P(A)P(B)
- la independencia entre eventos se extiende a sus complementos

teorema de la probabilidad total: permite calcula la probabilidad de un suceso B sumando las probabilidades de los distintos caminos o escenarios posibles que llevan a el
- los sucesos Ai deben ser excluyentes
- cubren todas las opciones posibles
$$𝑃(𝐵) = ∑_{i=1}^{n}𝑃(𝐴𝑖 )𝑃(𝐵/𝐴𝑖)$$
### teorema de bayes
es una manipulacion de la probabilidad condicional y del teorema de la probabilidad total
$$𝑃(𝐴_i/𝐵) = \frac{𝑃(𝐴_i)\,𝑃(𝐵/𝐴_i)}{\sum_{i=1}^{n} 𝑃(𝐴_i)\,𝑃(𝐵/𝐴_i)}$$

a pesar de su simpleza es muy importante: base de la inferencia bayesiana, permite afinar probabilidades (posiblemente subjetivas) incorporando informacion observada en la realidad

tip con arbol: multiplicar los tramos de la rama buscada y dividir por la probabilidad total del suceso condicionante
# variable aleatoria
es una funcion matematica que asigna un valor numerico a cada resultado de un experimento al azar. Se describe como X

variable aleatoria discreta: para espacios muestrales discretos
- se asigna funcion masa de probabilidad que dice la probabilidad exacta de que la variable sea igual a un valor especifico
variable aleatoria continua: para espacios muestrales continuos
- se asigna funcion densidad. Significa la concentracion de probabilidad en un punto

condiciones que deben cumplir:
- funcion masa: $$0 \le P(X=x_i) \le 1 \quad ; \quad \sum_i P(X=x_i) = 1$$
- funcion densidad: $$f(x) \ge 0 \quad ; \quad \int_{-\infty}^{\infty} f(x)\,dx = 1$$

para asignar probabilidades a una variable aleatoria es construir su distribucion de probabilidades. esta representa un modelo teorico que describe la forma en que varian los resultados de un experimento aleatorio

para el ejemplo de las caras de la moneda:

| X: numero de caras | 0   | 1   | 2   |
| ------------------ | --- | --- | --- |
| P(x): funcion masa | 1/4 | 1/2 | 1/4 |

funcion de distribucion acumulada calcula la probabilidad de que una variable aleatoria tome un valor igual o menor a un numero especifico
$$F(x_0) = P(X \le x_0) = \sum_{x_i \le x_0} P(x_i) \quad \text{o} \quad \int_{-\infty}^{x_0} f(x)\,dx$$

propiedades de F(x):
- lim_{x→-∞} F(x) = 0 ; lim_{x→∞} F(x) = 1
- no decreciente
- continua a derecha
- en continuas: F'(x) = f(x) (teorema fundamental del calculus)

probabilidades en intervalos:
$$P(a < X \le b) = F(b) - F(a)$$
en continuas P(X=x) = 0 (area de un solo punto es cero), asi que incluir o no los extremos da igual

#### esperanza de una variable aleatoria v.a.
es una medida de tendencia central. es un promedio ponderado que la variable puede tomar, en el que los pesos son las respectivas probabilidad o valores de densidad

- si x es discreta: $$𝑬(𝑿) = 𝝁 = ∑_𝒊 𝒙_𝒊𝑷(𝑿 = 𝒙_𝒊)$$
- si x es continua: $$𝑬(𝑿) = 𝝁 = ∫_{-\infty}^{\infty} 𝒇(𝒙)𝒅x$$
##### propiedades de la esperanza
Propiedades de la esperanza Sean 𝑋 e 𝑌 variables aleatorias y 𝑐 un número real 
- 𝐸(𝑐) = 𝑐 
- 𝐸(𝑋 + 𝑐) = 𝐸(𝑋) + 𝑐 
- 𝐸(𝑐𝑋) = 𝑐𝐸(𝑋) 
- 𝐸(𝑋 + 𝑌) = 𝐸(𝑋) + 𝐸(𝑌) 
- 𝐸(𝑋 − 𝑌) = 𝐸(𝑋) − 𝐸(𝑌) 
- Si X e 𝑌 son independientes 𝐸(𝑋𝑌) = 𝐸(𝑋) ⋅ 𝐸(𝑌)

### varianza de una variable aleatoria
la varianza constituye una medida de dispersion de los valores de X alrededor de la esperanza matematica de X
$$𝑽𝒂𝒓(𝑿) = 𝝈^𝟐 = 𝑬(𝑿 − 𝝁)² = 𝑬(𝑿^𝟐 ) − 𝑬(𝑿)^𝟐$$
para calcularla hace falta previamente E(X^2):
- discreta: $$E(X^2) = \sum_i x_i^2\,P(X = x_i)$$
- continua: $$E(X^2) = \int_{-\infty}^{\infty} x^2 f(x)\,dx$$

#### varianza propiedades
sean X e Y variables aleatorias y c un numero real (constante)
- 𝑉 (𝑐 ) = 0 
- 𝑉(𝑋 + 𝑐) = 𝑉(𝑋) 
- 𝑉(𝑐𝑋) = 𝑐 2𝑉(𝑋) 
- Si 𝑋 e 𝑌 son independientes 𝑉(𝑋 + 𝑌) = 𝑉(𝑋) + 𝑉(𝑌) 
- Si 𝑋 e 𝑌 son independientes 𝑉(𝑋 − 𝑌) = 𝑉(𝑋) + 𝑉(𝑌)

## variable aleatoria conjunta
un fenomeno puede requerir dos o mas variables aleatorias relacionadas. para estos casos se usa un conjunto de dos o mas variables aleatorias definidas sobre el mismo espacio muestral que analizan la probabilidad que ocurran ciertos valores de manera simultanea

funcion de probabilidad conjunta: es la probabilidad de que cada una de sus dimensiones sean menores o iguales a valores especificos de sus componentes
$$𝑭_{𝑿𝒀}(𝒙, 𝒚) = 𝑷[𝑿 ≤ 𝒙, 𝒀 ≤ 𝒚]$$
%%>que carajo significa esto?%%
para variables aleatorias conjuntas discretas (se pueden contar en cada una de las dimensiones), la probabilidad tambien puede definirse con la **funcion de masa conjunta**, que expresa la probabilidad de que ambas dimensiones tomen valores especificos de X y de Y
$$P_{𝑿𝒀}(𝒙, 𝒚) = 𝑷[𝑿 = 𝒙, 𝒀 = 𝒚]$$

las dimensiones son cada una de las variables aleatorias que componen la distribucion conjunta
propiedades de la funcion:
- 𝑃(𝑋 = 𝑥𝑖 , 𝑌 = 𝑦𝑗) ≥ 0 ∀𝑥𝑖 , 𝑦𝑗 
- ∑ ∑ 𝑃(𝑋 = 𝑥𝑖 𝑥 , 𝑌 = 𝑦𝑗) = 1
%%> que son las dimensiones? %%

la funcion de probabilidad conjunta de una variable aleatoria conjunta corresponde a la probabilidad de que cada una de sus dimensiones sean menores o iguales a valores especificos de sus componentes:
$$𝐹_{𝑋𝑌} = 𝑃(𝑋 ≤ 𝑥, 𝑌 ≤ 𝑦) = ∑ ∑ 𝑃(𝑋 = 𝑥_𝑖 , 𝑌 = 𝑦_𝑗)$$
esta funcion es no decreciente y toma valores en el intervalo cerrado \[0,1]

### distribuciones marginales
se llaman asi porque salen de los margenes de la tabla de distribucion conjunta: la probabilidad de una variable sin importar el valor de la otra
- P_X(xi) = ∑_j P(X=xi, Y=yj)
- P_Y(yj) = ∑_i P(X=xi, Y=yj)

### distribuciones condicionales
probabilidad condicional aplicada a variables: la conjunta dividida la marginal de la condicion
$$P(X/Y=y_j) = \frac{p_{XY}(x_i,y_j)}{P_Y(y_j)}$$
dada esta nueva v.a. se definen igual su esperanza y varianza condicionadas

### independencia entre variables aleatorias
$$P(X=x_i/Y=y_j) = P(X=x_i) \iff p_{XY}(x_i,y_j) = P_X(x_i)\cdot P_Y(y_j)$$
la conjunta es el producto de las marginales
basta encontrar UN par (xi, yj) que no cumpla para descartar independencia

todo lo anterior se extiende de forma natural a variables continuas: densidad conjunta, marginales y condicionales (integrales en vez de sumas)

### relacion lineal entre dos v.a.
covarianza: medida de la variacion conjunta entre dos variables, dos a dos
$$Cov(X,Y) = E(XY) - E(X)E(Y)$$
- positiva: crecen o decrecen juntas (nube creciente)
- negativa: cuando una crece la otra tiende a decrecer (nube decreciente)
- repartida alrededor de 0: sin relacion lineal
desventajas: depende de las unidades de medida y no esta acotada, no permite decir si la relacion es alta o baja

coeficiente de correlacion: normaliza la covarianza para cuantificar la relacion lineal
$$r = \frac{Cov(X,Y)}{S_x S_y} \text{(muestral)} \qquad \rho = \frac{Cov(X,Y)}{\sigma_x \sigma_y} \text{(poblacional)}$$
toma valores entre -1 y 1:
- r = 1: dependencia funcional lineal directa perfecta (recta creciente)
- 0 < r < 1: correlacion positiva, mas fuerte cuanto mas cerca de 1
- r = 0: sin correlacion lineal (pero puede existir otra dependencia funcional, ej cuadratica)
- -1 < r < 0: correlacion negativa (inversa)
- r = -1: dependencia funcional inversa perfecta (recta decreciente)
se analiza con diagramas de dispersion
