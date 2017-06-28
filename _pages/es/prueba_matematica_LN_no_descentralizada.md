---

layout: page
title: Prueba matemática que la red Lightning Network no conseguirá ser una solución descentralizada de escalabilidad para Bitcoin
permalink: /es/prueba_matematica_LN_no_descentralizada/

---

#### Por: [Jonald Fyookball](https://medium.com/@jonaldfyookball?source=post_header_lockup)

¿Has oído hablar de la red [Lightning Network para Bitcoin](https://lightning.network/lightning-network-paper.pdf)? Es una propuesta que afirma que:

> _“Utilizando una red de estos canales de micropago, Bitcoin puede escalar a billones de transacciones por día.”_

**Lo que no te están diciendo es que eso sólo puede lograrse utilizando grandes polos “bancarios” centralizados.**

Muchas personas en la comunidad de Bitcoin han supuesto erróneamente, o fueron llevados a creer, que la red “Lightning Network” (LN) sería una red _peer-to-peer_ (P2P) distribuida.

Sin embargo, eso es imposible. En efecto, demostraremos aqui que – aun utilizando un conjunto de supuestos bastante generosos – eso es imposible en el sentido matemático.

Este documento será divido en secciones. La **primera parte** dará una breve visión general de la red LN. La **segunda parte** explicará en términos sencillos por qué la red LN no conseguirá proporcionar escalabilidad descentralizada. Y la **tercera parte** dará una prueba matemática más rigurosa.

## PARTE I: VISIÓN GENERAL DE LA RED “LIGHTNING NETWORK” (LN)

### El debate acerca la escalabilidad de Bitcoin

[Bitcoin fue diseñado originalmente como un dinero peer-to-peer que escalaría usando aumentos simples en el tamaño de bloque.](https://keepingstock.net/an-open-letter-to-bitcoin-miners-c260467e1f0) Sin embargo, la discusión sobre cómo escalar la red se ha vuelto mucho más complicada y polémica.

[57 desarrolladores de Bitcoin “Core”](https://bitcoincore.org/en/2015/12/21/capacity-increase/) han firmado su apoyo a una [hoja de ruta oficial para aumento de capacidad](https://lists.linuxfoundation.org/pipermail/bitcoin-dev/2015-December/011865.html), que defiende la red Lightning Network como un “mecanismo de escalamiento sin aumento de uso ancho de banda” que pueda proporcionar una “descentralización muy alta”.

No compartimos esta opinión, y demostraremos que la red LN no conseguirá este objetivo. Después de leer y comprender la información aquí, recomendamos que saques tus propias conclusiones.

### ¿Qué es la red Lightning Network, y cómo funciona?

La red Lightning Network (LN) es un protocolo que permite una serie de **canales de pago bidireccionales** _fuera de cadena_. [Aquí está una excelente serie de 3 partes de Aaron van Wirdum](https://bitcoinmagazine.com/articles/understanding-the-lightning-network-part-building-a-bidirectional-payment-channel-1464710791/), si quisieras entender los aspectos técnicos.

“Bidireccional” significa simplemente “en dos sentidos”, donde Alice y Bob podrían abrir un canal privado y enviar bitcoins de un lado para otro (_fuera de la cadena_ de bloques):

![canal de pago bidireccional entre Alice y Bob](/images/es/prueba_matematica_LN_no_descentralizada/image1.png)

Para abrir el canal, una o ambas partes tienen que depositar bitcoins en una dirección especial de Bitcoin. [1] Después de eso, pueden hacer tantas transacciones como quieran dentro del canal, hasta que cualquiera de las partes decida cerrarlo, liquidándolo (pagando los saldos finales apropiados) en la cadena de bloques principal de Bitcoin.

### Vinculación de varios canales

Dando un paso más allá, si Alice tiene un canal con Bob, y Bob también tiene un canal con Carol, Alice podría indirectamente enviar dinero a Carol: primero Bob pagaría a Carol, y luego Alice le reembolsaría a Bob.

![canales de pago bidireccionales entre Alice y Bob y Carol](/images/es/prueba_matematica_LN_no_descentralizada/image2.png)

### La red prevista

Los evangelistas de la red LN promueven la idea de que si Alice puede pagar a Carol a través de Bob, deberíamos ser capaces de seguir extendiendo esta idea para construir toda una red de canales de pago, permitiendo así que un gran porcentaje de transacciones ocurra _fuera de cadena_.

Sin embargo, esto no se puede lograr realistamente como una red _peer-to-peer_ – al menos no una red de tamaño significativo.

### La semántica de “descentralizado” versus “distribuido”

En la discurso cotidiano sobre Bitcoin, la mayoría de la gente dice “descentralizado” para significar lo que técnicamente es una “topología distribuida”.

Por el contrario, una red con concentradores centralizados puede técnicamente llamarse “descentralizada” si no tiene un centro singular.

Pero no nos dejemos atrapar por los juegos de palabras. El siguiente diagrama [2] debe aclarar las cosas:

![cómo LN realmente parecerá, y como las personas piensan que LN debería parecer (¡no es posible!)](/images/es/prueba_matematica_LN_no_descentralizada/image3.png)

## PARTE II: UNA EXPLICACIÓN PARA “LEGOS”: POR QUE LA LIGHTNING NETWORK NO CONSEGUIRÁ ESCALAR

Voy a hacer esta explicación lo más breve posible.

Primero, tienes que entender que la red Lightning Network no es como otras redes – porque no puedes simplemente conectarte a otro usuario cuando quieras.

Para enviar o recibir bitcoins, necesitas o bien un **canal de pago** con ese usuario específico, o bien una serie conectada de canales de pago (una **“ruta”**).

No tiene sentido crear un canal de pago con el único propósito de enviar una transacción _fuera de cadena_, ya que requiere una transacción _en cadena_ para abrir el canal (y otra transacción para cerrarlo). También podrías al contrario enviar una transacción _en cadena_; no necesitas la red LN.

La idea es que se supone que eres capaz de enrutar tu pago a cualquier destino a través de una serie de conexiones. Desde el punto de vista de un usuario, la ruta potencial a cualquier persona se ve como una estructura de árbol:

![estructura de árbol](/images/es/prueba_matematica_LN_no_descentralizada/image4.png)

### Comienza como un problema básico de matemáticas

Vamos a suponer que el objetivo es escalar a un millón de usuarios.

Pensemos en esto: Si tienes un árbol con 10 ramas, y cada una de esas ramas tiene 10 hojas, puede llegar a 100 hojas.

Y si tienes un árbol con 10 ramas, y cada una tiene 10 sub-ramas, y cada una de ellas a su vez tiene 10 sub-ramas, etc ... puede llega a 6 niveles de “profundidad” y obtener: 10 x 10 x 10 x 10 x 10 x 10, o simplemente: 10^6, lo que equivale a un millón.

Puesto que tienes que saltar de rama a rama 6 veces para alcanzar la hoja, podemos decir que tenemos “6 saltos”. Entonces son 10 ramas con 6 saltos, o en nuestro caso: 10 canales con 6 saltos.

Entonces, ¿cuál es el problema?

### Tu dinero no puede estar en dos lugares al mismo tiempo

Si asumimos que necesitamos 10 canales de pago para alcanzar toda la red en 6 saltos, eso significa que tendrías que dividir tus bitcoins en 10 porciones.

Sin embargo, probablemente sólo uno de estos canales llegará al destinatario en cualquier momento. Eso significa que sólo podrás enviar parte de tu dinero, por ejemplo unos 10%.

¿Podríamos evitar esto simplemente con 2 canales y, digamos, 20 saltos? Volveremos a esta pregunta. En primer lugar, vamos a entender otro hecho importante:

### Todo el mundo está concediendo préstamos a todos los demás

Imagina que Alice quiere enviar 1 BTC a Carol através Bob así: Alice -> Bob -> Carol

Con el fin de encaminar el dinero, **Bob tiene que tener al menos 1 BTC en su “saldo” en el canal con Carol**. Esencialmente, Alice está pidiendo prestado a Bob para pagar a Carol.

Bob transfiere su 1 BTC a Carol en el canal [Bob -> Carol], y Alice transfiere 1 BTC a Bob en el canal [Alice -> Bob]. Así es como funciona – Alice no puede “dar” el 1 BTC a Bob para luego pasar a Carol.

Realmente es un préstamo porque la red usa bloqueos de tiempo para eliminar el riesgo de custodia: **Alice no puede pagar a Bob con seguridad hasta que esté segura de que Bob ha pagado a Carol.**

De hecho, cada salto en ruta a un destino debe tener los fondos disponibles para cada transacción. Por lo tanto, cuanto más saltos se utilizan, más esta carga de préstamos se multiplica.

¿Por qué es eso un gran problema?

**Eso significa que un gran número de saltos quiebra el proceso**

Digamos que todo el mundo estaba utilizando rutas con 20 saltos, y la mayoría de los usuarios gastan alrededor de $ 1000 / mes. Si cada uno hiciera su parte justa para ayudar a los pagos de la ruta, cada usuario necesitaría encaminar $ 20.000 / month.

¿Eso sería posible?

Depende de muchos factores, incluyendo: la cantidad de tiempo requerido para una ruta y el número de transacciones.

Incluso si hacemos un supuesto (posiblemente generoso) de que un usuario pueda enrutar 20 veces su carga de transacción normal y sólo sufra una reducción del 50% en la disponibilidad de sus canales, entonces necesitaría duplicar el número de canales que normalmente tendría.

**En realidad, es peor aun**

Hay al menos 5 problemas adicionales que empeoran la situación.

1.  Incluso la matemática básica de 10^6 = 1.000.000 con la que empezamos no es aplicable. Si asumimos que los compañeros forman conexiones generalmente aleatorias sin una autoridad central para planificar las rutas, entonces hay cierta probabilidad de éxito. Una oportunidad de uno en un millón, repetida un millón de veces, sólo produce una tasa de éxito del 63%. La elección de 2 millones de veces mejora esto al 84%, lo que significaría aumentar el número de canales. [3]

2.  A medida que los usuarios gastan sus ingresos, las rutas disponibles se degradan, hasta el momento en que se depositan más fondos. En otras palabras, cuando una persona recibe un pago salarial y deposita fondos en la red, sus canales están al máximo, con el poder de enrutamiento completo. Pero a medida que su dinero se gasta, este poder cae hacia cero. Calculado en promedio, este patrón corta la potencia de enrutamiento en aproximadamente la mitad, lo que requiere el doble del número de canales.

3.  El enrutamiento de fondos para terceros interrumpe la distribución uniforme de los fondos, lo que también disminuye el número de canales utilizables.

4.  Hay una gran disparidad de riqueza en cualquier población. Por lo tanto, el número de usuarios que pueden encaminar fondos para cualquier otro usuario aleatorio es sólo una fracción de la red. Y este problema se magnifica exponencialmente con un número creciente de saltos.

5.  Siempre existe el riesgo de que un canal de enrutamiento no responda (intencional o involuntariamente). Este riesgo también crece exponencialmente con un número creciente de saltos.

### En resumen (“TL;DR”)

Para llegar a cualquier persona en una red grande con una serie de conexiones ramificadas de canales, necesita un gran número de canales o un gran número de saltos.

Ambos son un problema enorme. Un gran número de canales significa que los usuarios tienen que dividir sus fondos y no pueden hacer nada excepto pequeñas compras. Y un gran número de saltos significa que el dinero de todo el mundo estará inmovilizado haciendo enrutamiento para el dinero de todos los demás.

### Conclusión: Un sistema completamente imposible de funcionar

A medida que la red llega a un millón de usuarios, parece que no habrá una manera realista de evitar estos problemas. La división de fondos entre muchos canales y la concesión constante de préstamos de dinero harán que la red sea inutilizable.

Las únicas visiones concebibles son: (a) todo el mundo tendrá que depositar mucho más de lo que necesitan para realizar transacciones, o (b) el sistema tendrá que depender de grandes centros centralizados.

Tampoco es una solución de escalabilidad descentralizada – ni siquiera um componente singificativo de una tal solución.

## PARTE III: PRUEBA MATEMÁTICA INFORMAL

### 1. Supuestos

Obviamente, no se puede modelar una red teórica de un gran grupo de personas diversas que no existe en realidad. Reconocemos hacer una serie de supuestos, algunos declarados, algunos implícitos, y algunos generosos a los críticos de esta prueba.

En este contexto, pretendemos demostrar, a través de cálculos de probabilidad, que se necesitará un gran número de canales de pago abiertos para cada usuario, haciendo que el sistema sea esencialmente inoperable a un tamaño de 1.000.000 de usuarios.

### 2. Canales y saltos necesarios, sin restricciones

Modelando la red como un grafo complejo de 1.000.000 nodos, examinaremos la probabilidad de alcanzar un par arbitrario, dado un cierto número de canales abiertos, C, y permitiendo un cierto número de saltos, H.

Desde la perspectiva de un usuario, llegar a pares lejanos a través de una serie de canales de ramificación es similar a una estructura de árbol. [4] El número de hojas crece exponencialmente, y son posibles destinos de transacción.

Para simplificar los cálculos, ignoraremos la posibilidad de que una rama en el árbol pueda vincularse a otra rama que ya está en el árbol (como un antepasado o un primo).

El acontecimiento de esta posibilidad reduciría el número de pares encontrados, de una ramificación puramente exponencial a un número levemente más bajo. Puesto que estamos tratando de demostrar que un número relativamente bajo de pares sería alcanzado sin un gran número de canales o saltos, y el número real sería aun más bajo, esta es un supuesto generoso (que fortalece la prueba).

Sea n el número de hojas, definido como C^H. Por ejemplo, 10 canales abiertos y 6 saltos son 10^6 = 1.000.000.

La probabilidad P de no elegir un miembro de un conjunto \|N\| con cardinalidad n por muestreo n veces, con reemplazo es:

![ecuación: elegir un miembro de un conjunto N con cardinalidad n por muestreo n veces](/images/es/prueba_matematica_LN_no_descentralizada/image5.png)

(En nuestro caso, alcanzar un destino deseado que coincida con una hoja.)

Podemos generalizar esto con la forma límite:

![ecuación: generalización con forma de limite](/images/es/prueba_matematica_LN_no_descentralizada/image6.png)

Dado que 1 / e = 0,3678... entonces la probabilidad de elegir correctamente al menos una vez es (1- (1 / e)) = 63,21...%

Una tasa de acceso a cualquier par de sólo 63.21% es demasiado bajo para ser considerado como exitoso para un sistema de pago.

El uso de un número diferente de ensayos se puede expresar como:

![ecuación: uso de un número diferente de ensayos](/images/es/prueba_matematica_LN_no_descentralizada/image7.png)

Por ejemplo:

![ecuación: ejemplo de uso de un número diferente de ensayos](/images/es/prueba_matematica_LN_no_descentralizada/image8.png)

Tomando varios exponentes de e, podemos calcular las probabilidades correspondientes:

![tabla: probabilidades usando varios exponentes de e](/images/es/prueba_matematica_LN_no_descentralizada/image9.png)

Utilizando un valor de 1.000.000 de usuarios y la forma límite, derivamos la fórmula:

![fórmula: 1.000.000 de usuarios e forma limite](/images/es/prueba_matematica_LN_no_descentralizada/image10.png)

Utilizando esta fórmula, podemos calcular algunos valores iniciales que alcancen al menos el nivel de probabilidad del 80%; sin embargo, esto no está tomando en cuenta otros factores aún no discutidos:

![tabla: valores iniciales que alcancen al menos el nivel de probabilidad del 80%](/images/es/prueba_matematica_LN_no_descentralizada/image11.png)

### 3. Canales y saltos necesarios, con una restricción monetaria básica

Todos los saltos a lo largo de la ruta deben tener fondos suficientes para procesar cualquier pago que deseen servir. Esta es la _restricción monetaria_.

No es posible modelar precisamente una red de un millón de usuarios con una amplia variedad de perfiles financieros y patrones de gasto porque hay demasiados factores desconocidos.

Sin embargo, podemos hacer una suposición muy general, de sentido común, de que muchos o la mayoría de los usuarios recibirán algún tipo de ingreso en algún tipo de intervalo regular y depositarán una subsidio de fondos en la redLN para gastar.

Los fondos depositados generalmente serán gastados o eventualmente retirados. (Supondremos que la red LN no se utiliza como un vehículo de ahorro.)

A medida que los usuarios gastan los fondos, la disponibilidad de los canales de pago para el enrutamiento se degradará, ya sea porque se cierra un canal o porque la cantidad financiada disminuye. Cuando se depositan fondos adicionales, se revitalizan las capacidades de enrutamiento.

No disponemos de un modelo detallado de cuáles y cuántos usuarios están recebiendo cuánto, cuándo y con cuál frecuencia. Sin embargo, podemos agregar el comportamiento del conjunto de usuarios gracias a la ley de grandes números, que establece que “el promedio de los resultados obtenidos de un gran número de ensayos debe estar cerca del valor esperado”.

El ciclo típico de consumo consiste en recibir ingresos, gastarlos y luego repetir el proceso. Podemos generalizar este comportamiento como una onda de diente de sierra inversa:

![ecuación: onda de diente de sierra inversa](/images/es/prueba_matematica_LN_no_descentralizada/image12.png)

Visualmente, aparece como:

![gráfica: onda de diente de sierra inversa](/images/es/prueba_matematica_LN_no_descentralizada/image13.png)

Los pagos salariales se representan por los picos, y los ingresos se gastan gradualmente hasta el próximo pago.

La integración de la función da la mitad del valor del período, como se esperaba:

![ecuación: integral de la onda de diente de sierra inversa](/images/es/prueba_matematica_LN_no_descentralizada/image14.png)

Esto también es evidente visualmente, porque las ondas forman triángulos rectos recortando la mitad del área.

La implicación es que aproximadamente la mitad de los canales que se utilizarían para el enrutamiento no son válidos. Por lo tanto, el número de canales en cada salto (“hop”)  tiene que ser duplicado.

Nuestra fórmula de probabilidad se convierte en:

![fórmula: número de canales en cada salto, duplicado](/images/es/prueba_matematica_LN_no_descentralizada/image15.png)

Y nuestra tabla de resultados se convierte en:

![tabla: número de canales en cada salto, duplicado](/images/es/prueba_matematica_LN_no_descentralizada/image16.png)

**También hay una supuesto generoso muy grande que estamos haciendo**, que es que todos los usuarios forman una parte útil del conjunto de participantes de enrutamiento para todos los demás usuarios. En realidad, una distribución muy desigual de riqueza probablemente pondría restricciones adicionales y significativas al sistema.

### 4. Restricción adicional a la concesión de préstamos

Además de las cargas de división de fondos y búsqueda de rutas, suponemos que el usuario también participa en la red, ayudando a otros en el enrutamiento de pagos.

Esto incomoda al usuario de dos maneras.

En primer lugar, esto puede hacer que la distribución de los fondos personales del usuario se vuelva desequilibrada, disminuyendo el número de rutas disponibles. Con el tiempo, esto podría teóricamente establecer una media, con el dinero fluyendo en cualquier sentido de cualquier canal específico. Sin embargo, cada usuario estaría sujeto a un gran grado de varianza en cualquier momento específico.

En segundo lugar, el dinero utilizado en el enrutamiento de los pagos para otros no está disponible para el usuario durante el tiempo que la ruta está en uso.

Ignoraremos generosamente la primera causa de incomodidad y sólo intentaremos modelar la segunda. Tomaremos el enfoque simplista de asumir que todos los usuarios tienen el mismo número promedio de transacciones y volumen de gasto, y asumimos que cada usuario participa igualmente en el enrutamiento.

Definamos las siguientes variables:

U: el número de usuarios

H: el número de saltos

V: el volumen total de transacciones de la red durante un período de tiempo

v: el volumen de transacciones por usuario durante un período de tiempo

r: el volumen enrutado total por usuario durante un período de tiempo

D: la duración en horas de un período de tiempo de medición

t: el número medio de transacciones por usuario para el período D

d: la duración en horas de la ruta media

Puesto que cada salto necesita enrutar la cantidad de transacción entera para cualquier transacción en una ruta en la que participe, el volumen enrutado total para toda la red durante un periodo de tiempo = VH.

Así, r = VH / U. Y como V / U = v, r = Hv.

Por ejemplo, si v = $ 1000, el gráfico aparece como:

![gráfica: v = $ 1000](/images/es/prueba_matematica_LN_no_descentralizada/image17.png)

Introduzcamos el concepto de dólar-hora para medir la capacidad de enrutamiento.

Cada usuario sólo puede gastar su propio dinero una vez, obviamente. Pero con el propósito de enrutar el dinero de otros, podemos pensar en dólar-hora como el total de dólares en sus canales, multiplicado por el número de horas que están disponibles. Por ejemplo, $ 1000 sentados inmovilizados durante una semana es 168.000 dólares-horas.

Podemos entonces calcular un cociente Q, que representa el porcentaje de capacidad disponible que queda después del enrutamiento para otros:

Q = 1 – (d (H – 1)) / D

Tenga en cuenta que v y t no aparecen en la ecuación porque son eliminados usando división, pero están implícitos en la relación d / D. El motivo para H – 1 es que un salto no cuesta nada a la red más allá de las transacciones propias de un usuario (r = Hv).

Por ejemplo, si la red usa 4 saltos (“hops”) y las rutas requieren 4 horas, y los saldos del usuario para el enrutamiento se basan en 168 horas (1 semana), entonces:

Q = 1 – ((4) * (3)) / 168) = 0,92

Nuestra fórmula de probabilidad es ahora:

![fórmula: ahora](/images/es/prueba_matematica_LN_no_descentralizada/image18.png)

Suponiendo que D = 168, y el tiempo de enrutamiento d = 4 horas, llegamos a las siguientes probabilidades:

![tabla: D = 168, d = 4](/images/es/prueba_matematica_LN_no_descentralizada/image19.png)

### 5. Determinación de limitaciones de transacciones basadas en una distribución de Pareto

Casi no parece necesario probar que si los fondos necesitan ser divididos en pequeños baldes, habría un enorme efecto negativo en la usabilidad. Sin embargo, para completar, incluimos esta sección.

Asumimos que la mayoría de los gastos de consumo y de negocios siguen una distribución de Pareto donde cada usuario realiza un número relativamente pequeño de transacciones grandes, varias transacciones de tamaño medio y una cantidad mayor de transacciones más pequeñas.

La función de densidad de probabilidad de Pareto se expresa como:

![funcíon: probabilidad de Pareto](/images/es/prueba_matematica_LN_no_descentralizada/image20.png)

Para la curva de Pareto de tipo 1 más simple, esto se simplifica a:

![funcíon: probabilidad de Pareto, tipo 1, más simple](/images/es/prueba_matematica_LN_no_descentralizada/image21.png)

![gráfica: probabilidad de Pareto, tipo 1, más simple](/images/es/prueba_matematica_LN_no_descentralizada/image22.png)

La distribución no cambia con la aplicación de constantes, pero podemos visualizar mejor el modelo con algunos valores del mundo real multiplicando los valores de y por 1000 – de manera que las cantidades en dólares para los artículos costosos se vuelven significativas – y integrar sobre un conjunto típico de valores x (el número de transacciones a cada valor en dólares), digamos 50.

![ecuación: integral sobre un conjunto típico de valores x, digamos 50](/images/es/prueba_matematica_LN_no_descentralizada/image23.png)

La suma total de transacciones = $ 980. Usando un valor del 10% de $ 98, podemos resolver la ecuación: 98 = 1000 / x², para obtener 3,194 transacciones.

A continuación, vamos a integrar sobre el conjunto más pequeño de transacciones para obtener el valor de la suma de las transacciones que tienen cantidades inferiores a nuestro valor mínimo de $ 98:

![ecuación: integral sobre el conjunto más pequeño de transacciones](/images/es/prueba_matematica_LN_no_descentralizada/image24.png)

![gráfica: integral sobre el conjunto más pequeño de transacciones](/images/es/prueba_matematica_LN_no_descentralizada/image25.png)

Dado que 293.48 / 980 = .299, podemos decir que sólo el 29.9% de toda la actividad económica deseada sería posible si 10 canales fueran usados.

### Consideraciones finales

Estoy preparado para críticos puntillosos. Quisiera recomendarte a hacer tu propio pensamiento crítico. No olvides los supuestos generosos que hemos hecho para ignorar la disparidad de riqueza.

Recuerde, Bitcoin debe ser descentralizado. Tengas cuidado con la racionalización que dice que “la centralización sería algo soportable, siempre y cuando la capa base se mantiene descentralizada”. Eso sería una trampa insidiosa que permitiría obligar a los usuarios a salir de la capa base y entrar en sistemas centralizados. Nunca debemos permitir eso.

Entonces, ¿el Bitcoin está en apuros porque las soluciones de segunda capa pueden no funcionar? No, en absoluto. Bitcoin fue diseñado para escalar _en cadena_ con incrementos de bloques simples. Puede hacerlo y conseguirá hacerlo – si lo permitimos.

#### Notas

1.  No es un nuevo tipo de dirección. Simplemente, es una dirección multi-firma para los propósitos del canal.

2.  Originalmente publicado por Carl S. Sterner en 'Resilience and Decentralization'.

3.  Hay consideraciones de probabilidad adicionales como se discute en la parte III.

4.  Técnicamente un grafo complejo, no una estructura de árbol, aunque un árbol pueda servir de construcción mental apropiada.

#### Fuente

Artigo original en inglés: [Mathematical Proof That the Lightning Network Cannot Be a Decentralized Bitcoin Scaling Solution](https://medium.com/@jonaldfyookball/mathematical-proof-that-the-lightning-network-cannot-be-a-decentralized-bitcoin-scaling-solution-1b8147650800) - por [Jonald Fyookball](https://medium.com/@jonaldfyookball?source=post_header_lockup)

Hilo en [r/btc](https://www.reddit.com/r/btc) sobre el artigo original: [Game Over Blockstream: Mathematical Proof That the Lightning Network Cannot Be a Decentralized Bitcoin Scaling Solution (by Jonald Fyookball)](https://np.reddit.com/r/btc/comments/6jqrub/game_over_blockstream_mathematical_proof_that_the/) - enviado por [u/BitAlien](https://www.reddit.com/user/BitAlien)

Traducción del inglés al español por: [u/bitipedia](https://www.reddit.com/user/bitipedia)

Sugerencias y mejoras son [bienvenidas](https://bitipedia.github.io/en/about/) - especialmente de personas que sean hablantes nativos de español!
