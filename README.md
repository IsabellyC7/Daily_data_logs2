Hoje pela manhã participei da daily da Pernambucanas. Em seguida, subi meus arquivos de estudo no GitHub, já que ontem eu ainda estava com dúvida sobre qual repositório utilizar e acabei aguardando a reunião, e acabou não dando tempo. Aproveitei para subir o conteúdo de ontem, criar a feature referente ao dia de hoje e já deixei tudo preparado para ir atualizando ao longo do dia.

Depois disso, foquei nos estudos de PySpark, executando alguns códigos para treinar e reforçar o aprendizado na prática, que é a forma que eu mais aprendo. Como o curso está mais teórico, fiz algumas comparações com SQL, o que me ajudou bastante a entender melhor os conceitos, e já estou conseguindo aplicar comandos básicos.

Também estudei alguns conceitos importantes de PySpark e utilizei o Google Colab (conforme orientação do Brizola) para executar os códigos por partes, facilitando o entendimento de cada etapa.

No geral, fiquei bem satisfeita com o progresso de hoje, pois sinto que estou conseguindo compreender bem o conteúdo e evoluir de forma consistente.

Alguns códigos que fiz pra treinar:

```python
# teste basico, para gravar os comandos e entender melhor cada um

print("iniciando spark...") # teste

from pyspark.sql import SparkSession  # importando a classe do Spark

# começa a configurar o Spark
spark = SparkSession.builder \
    .appName("Teste") \  # define o nome da aplicação
    .getOrCreate()       # cria a sessão se não existir ou reutiliza se já tiver

print("spark iniciado")

dados = [("Isa", 17), ("João", 25)]  # criando dados: cada tupla é uma linha do DataFrame

df = spark.createDataFrame(dados, ["nome", "idade"])  # criando DataFrame

df.show()  # exibe o DataFrame no terminal (equivalente ao SELECT * FROM)

print("finalizando...")

spark.stop()

# teste com filter e adicionar coluna

from pyspark.sql import SparkSession
from pyspark.sql.functions import col  # permite acessar uma coluna do DataFrame

spark = SparkSession.builder.appName("Ex1").getOrCreate()

dados = [("Isa", 17), ("Faria", 22), ("JoãoC", 15), ("Enzo", 18), ("Juliane", 20)]
df = spark.createDataFrame(dados, ["nome", "idade"])

df.filter(df.idade >= 18)  # só filtra, não altera df até show

df = df.withColumn("ano_nascimento", 2026 - col("idade"))  # cria nova coluna

df.show()

spark.stop()