# Test-Semantix


1 - QUAL O OBJETIVO DO COMANDO CACHE EM SPARK?
Cache ou persistência são técnicas de otimização para cálculos Spark (iterativos e interativos). Eles ajudam a salvar resultados parciais intermediários 
para que possam ser reutilizados nos estágios subsequentes. Esses resultados provisórios como RDDs são, portanto, mantidos na memória (padrão) 
ou em armazenamentos mais sólidos, como disco e / ou replicados


___________________________________________________________________________________________________________________________________________________________

2 - O MESMO CÓDIGO IMPLEMENTADO EM SPARK É NORMALMENTE MAIS RÁPIDO QUE A IMPLEMENTAÇÃO EQUIVALENTE EM
MAPREDUCE. POR QUÊ?
Spark é geralmente mais rápido que o MapReduce devido à forma como processa os dados. Enquanto o MapReduce opera em etapas, 
o Spark opera a partir de todo o conjunto de dados de um só vez.


___________________________________________________________________________________________________________________________________________________________

3 - QUAL É A FUNÇÃO DO SPARKCONTEXT ?
O objeto SparkContext é reponsavel em informar ao Spark como acessar um cluster. 
COnforme exmplo em Python para criar um SparkContext você precisa criar um objeto SparkConf que contenha informações sobre seu aplicativo.

conf = SparkConf().setAppName(appName).setMaster(master)
sc = SparkContext(conf=conf)


___________________________________________________________________________________________________________________________________________________________

4 - EXPLIQUE COM SUAS PALAVRAS O QUE É RESILIENT DISTRIBUTED DATASETS (RDD).

É uma coleção de elementos particionados nos nós dos clusters que podem ser operados em paralelo.

___________________________________________________________________________________________________________________________________________________________

5 - GROUPBYKEY É MENOS EFICIENTE QUE REDUCEBYKEY EM GRANDES DATASET. POR QUÊ?

Seguindo exemplo da referencia utilizada para a resposta.

Em um arquivo teremos os seguintes dados:
Messi 45
Ronaldo 52
Messi 54
Ronaldo 51
Messi 48
Ronaldo 42

Utilizando o reduceByKey teremos o seguinte resultado:

myPair.reduceByKey { case (a, b) => a + b }.foreach { println }

(Messi,147)
(Ronaldo,145)

Utilizando o groupByKey teremos o seguinte resultado:

myPair.groupByKey().foreach(println)

(Messi,CompactBuffer(45, 54, 48))
(Ronaldo,CompactBuffer(52, 51, 42))

Quando um groupByKey é chamado em um par RDD, os dados nas partições são embaralhados na rede para formar uma chave e uma lista de valores. 
Esta é uma operação trabalhosa, particularmente quando se trabalha em um grande conjunto de dados. Isso também pode causar problemas quando a 
lista de valores combinados é enorme para ocupar em uma partição. Tesse caso podemos ter um derramamento de disco.


___________________________________________________________________________________________________________________________________________________________

6 - EXPLIQUE O QUE O CÓDIGO SCALA ABAIXO FAZ.

val textFile = sc . textFile ( "hdfs://..." ) 
val counts = textFile . flatMap ( line => line . split ( " " ))
. map ( word => ( word , 1 ))
. reduceByKey ( _ + _ )
counts . saveAsTextFile ( "hdfs://..." )

Esta fazendo a contagem de palavras e salvando em um arquivo.



