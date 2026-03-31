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
```

## 18/03/2026

Hoje foquei nos estudos práticos de PySpark, aplicando junto com a lógica de ETL (extract, transform e load), o que me ajudou a entender melhor como funciona um fluxo de dados na prática.

Trabalhei com leitura de arquivos CSV, junção de dados com join (bem parecido com SQL), criação de colunas calculadas e também agrupamentos com groupBy usando sum e count para gerar algumas métricas.

Também utilizei o Google Colab para rodar o código por partes, o que facilitou bastante o entendimento de cada etapa separadamente, ai adicionei comentários sobre o que cada parte fazia.

Além disso, comecei um desafio prático criando DataFrames manualmente, fazendo joins e aplicando transformações,porém não finalizei ainda, mas ajudou a fixar bem.

No geral, foi um dia bem focado em prática, e sinto que consegui evoluir bem no entendimento do PySpark.

Código ETL:

``` python
    from pyspark.sql import SparkSession
from pyspark.sql.functions import sum, count
print("RODOU O ARQUIVO")



spark = SparkSession.builder \
    .appName("Projeto Vendas") \
    .getOrCreate()

print("INICIANDO...")
# EXTRACT ler dados
#manda o Spark abrir um arquivo CSV / fala que a primeira linha tem os nomes das colunas / faz tentar descobrir os tipos / cria os dataframes
df_vendas = spark.read.csv("data/vendas.csv", header=True, inferSchema=True)
df_clientes = spark.read.csv("data/clientes.csv", header=True, inferSchema=True)
df_produtos = spark.read.csv("data/produtos.csv", header=True, inferSchema=True)
df_vendas.show()

# TRANSFORM

# Join junta as tabelas, tipo sql 
df = df_vendas.join(df_clientes, "id_cliente") \
              .join(df_produtos, "id_produto")

# KPI agrupa os dados por categoria/ soma o valor das vendas dentro de cada grupo/ conta quantas vendas existem/ renomeia a coluna
df_kpi = df.groupBy("categoria").agg(
    sum("valor").alias("total_vendas"),
    count("*").alias("quantidade_vendas")
)

print("MOSTRAR")
# SELECT * FROM mostra
df_kpi.show()

# LOAD a parte de salvar/ se já existir arquivo, substitui/ salva no formato padrão parquet/ pelo que entendi salva os dados em uma pasta 

df_kpi.write.mode("overwrite").parquet("output/relatorio_vendas")
```

## 19/03/2026

Hoje pela manhã participei da daily da Pernambucanas. Em seguida, entrei em uma reunião onde foi apresentada a nova demanda, junto com as instruções de como deveria ser realizada.

Após isso, iniciei a atividade que consiste em trabalhar com queries SQL no BigQuery, executando os códigos fornecidos, analisando os erros retornados e realizando os ajustes necessários para que as consultas funcionem corretamente. Durante esse processo, também comecei a me familiarizar com o ambiente do BigQuery e a entender melhor como os erros se comportam e como corrigi-los na prática.

## 23/03/2026

Hoje Iniciei a demanda que consiste em  
Transformar a view que ja existe, em um processo dataform que vai salvar numa tabela. Entrei em reunião com os meninos pra eles explicarem melhor sobre essa nova demanda.

Depois disso, tivemos que fazer alguns ajustes ali de permissões, no começo eu tive um pouco de dificuldade pra entender, porque nunca tinha mexido com Dataform, então ainda tava me situando. Aí entrei em call com o Brizola, e ele começou a me ajudar ali do zero, já iniciando uma parte da demanda comigo, então tá me dando uma baita força.

E se der tudo certo, hoje a gente deve continuar nisso pra eu conseguir seguir com a demanda 


## 24/03/2026
Hoje, segui na demanda de migrar a View para o Dataform. Comecei em call com o Brizola para dar continuidade à ajuda que ele estava me dando e, depois disso, consegui avançar sozinha na estruturação do código.

Tive um pouco de dificuldade no entendimento do SELECT final (como conectar as referências do WITH com a saída da tabela), então hoje meu foco é destravar essa parte, finalizar o script e rodar os testes em homologação."

## 26/03/2026
Hoje, passei boa parte do dia em call com a Elaine e o Brizola. Eles me deram um apoio gigante com as dúvidas que eu estava tendo e conseguimos dar uma boa continuidade na demanda.

Queria deixar um agradecimento especial /valeu para a Elaine, porque com a ajuda dela eu finalmente consegui entender a lógica do que eu estava fazendo, e não só executar e pro Brizola também. No finalzinho da tarde, tivemos um probleminha técnico — provavelmente um conflito pelo fato de a tabela ter o mesmo nome da view — então hoje meu foco é resolver esse detalhe e finalizar o processo."



## 27/03/2026

Hoje, finalizei a construção da tabela v_cota_produto_financeiro em call com o Brizola e a Elaine. Realizamos os testes e os dados estão retornando exatamente como o esperado.

Tínhamos uma dúvida sobre o conflito de nomes, já que a tabela estava substituindo a view, mas a Elaine validou com a Mai e a Bia e seguiremos com esse padrão mesmo, sem impedimentos.

Com isso, já dei início à próxima demanda, que é a view dominio_status. Estou estudando a melhor lógica para o particionamento dela; agora que compreendo melhor o processo, quero tentar estruturar essa parte sozinha antes de pedir uma revisão.

## 30/03/2026

Ontem eu  na sequência, realizei os KTs com o Brizola e o Lucas sobre o processo_log e a estrutura do Dataform, o que me ajudou a alinhar melhor esses processos.

Depois disso, dei continuidade no desenvolvimento da tabela viw_dominio_status. Para isso, utilizei a lógica de particionamento por num_anomes_prod, seguindo o mesmo padrão da v_cota_produt_financeiro.

Além do particionamento mensal, implementei também o CLUSTER BY st_id_status, por ser o principal campo de identificação da tabela. A ideia é otimizar a performance das consultas, já que os dados ficam organizados por esse ID dentro de cada partição mensal, tornando os filtros por status mais rápidos e eficientes.

## 31/03/2026

Hoje, tive uma reunião sobre o novo projeto que fui adicionada, que é sobre a criação de um GED para a digio.
logo após a reunião eu dei continuidade a minha demanda e acredito que acabei o script, porem executei e esta dando um erro no get_processo_log que não entendi, então estou esperando a disponibilidade dos meninos pra me ajudarem com esse erro.
Depois disso eu dei uma estudada sobre o que a Bia havia sugerido e segue um pouco doque vi sobre a ideia de "Agentes Inteligentes para Automação de Consultas e Facilitação do Acesso aos Dados":

Eu dei a ideia pra bia "de Agentes Inteligentes para Automação de Consultas e Facilitação do Acesso aos Dados"
e ela me retornou sobre o MCP do bigquerry que é um a gente que lista, analisa as descriçoes, e retorna oque foi pedido.
Eu achei muito interessante pq voce não precisa saber sql e nem nada do tipo para utilizar, pois ele utiliza linguagem natural, porem, pra conseguir implementar e tudo mais voce precisa de um desenvolvedor, claro, porque enfim tem que implementar o servidor e enfim.
e ele não é muito bem um chat, entao ele não vai explicar nada e enfim nada do tipo, ele não tem um front como se fosse um chat q é oq eu havia pensado pra ideia de agente que eu sugeri pra bia
entao meu objetivo é aprimorar a ideia pra que eu consiga usar o mcp como uma ponte pra um possivel projeto maior.

 




