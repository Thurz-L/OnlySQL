# **Módulo 2** | SQL: Trabalhando com Tabelas

## Atividades

### **1. Explorando os dados da tabela de clientes**

#### [**1.1. Query 1**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_1.csv)
```sql
SELECT id,
	idade,
	sexo,
	dependentes
FROM clientes;
```

#### [**1.2. Query 2**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_2.csv)
```sql
SELECT id,
	valor_transacoes_12m
FROM clientes
WHERE escolaridade = 'mestrado'
	and sexo = 'F';
```

#### [**1.3. Query 3**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_3.csv)
```sql
SELECT sexo,
	AVG(idade) AS "media_idade_por_sexo"
FROM clientes
GROUP BY sexo;
```

### **2. Inserindo novos dados**

#### [**2.1. Query 4**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_4.csv)
```sql
SELECT *
FROM clientes;
```

### **3. Criando e trabalhando com partições**

#### [**3.1. Query 5**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_5.csv)
```sql
CREATE EXTERNAL TABLE clientes_part(
	id BIGINT,
	idade BIGINT,
	dependentes BIGINT,
	escolaridade STRING,
	tipo_cartao STRING,
	limite_credito DOUBLE,
	valor_transacoes_12m DOUBLE,
	qtd_transacoes_12m BIGINT
)
PARTITIONED BY (sexo string)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
	'separatorChar' = ',',
	'quoteChar' = '"',
	'escapeChar' = '\\'
)
STORED AS TEXTFILE
LOCATION 's3://bucket-robertohatiro-partitioned/'
```

```sql
MSCK REPAIR TABLE clientes_part;
```

```sql
select *
from clientes_part
where sexo = 'F';
```

#### [**3.2. Query 6**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_6.csv)
```sql
SELECT id,
	idade,
	limite_credito
FROM clientes_part
WHERE sexo = 'M'
ORDER BY limite_credito DESC;
```

### **4. Adicionando colunas**

#### [**4.1. Query 7**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2002/query_7.csv)
```sql
ALTER TABLE clientes
ADD COLUMNS (estado string)
```

```sql
SELECT *
from clientes
```
