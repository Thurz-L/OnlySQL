# **Módulo 3** | SQL: Selecionando & Ordenando

### **2. Selecionando dados**

```sql
CREATE EXTERNAL TABLE transacoes (
	id_cliente BIGINT,
	id_transacao BIGINT,
	valor FLOAT,
	id_loja STRING
)
ROW FORMAT SERDE 'org.apache.hadoop.hive.serde2.OpenCSVSerde'
WITH SERDEPROPERTIES (
	'separatorChar' = ',',
	'quoteChar' = '"',
	'escapeChar' = '\\'
)
STORED AS TEXTFILE
LOCATION 's3://bucket-robertohatiro-transacoes/'
```

#### [**2.1. Query 1**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2003/query1.csv)
```sql
SELECT *
FROM transacoes
```

#### [**2.2. Query 2**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2003/query2.csv)
```sql
SELECT id_cliente,
	valor,
	id_loja AS nome_loja
FROM transacoes;
```

#### [**2.3. Query 3**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2003/query3.csv)
```sql
SELECT DISTINCT id_loja AS nome_loja
FROM transacoes;
```

### **3. Ordenando e limitando dados**

#### [**3.1. Query 4**](https://raw.githubusercontent.com/Thurz-L/OnlySQL/main/EBAC%20-%20SQL%20para%20Análise%20de%20Dados/Módulo%2003/query4.csv)
```sql
SELECT id_cliente,
	valor
FROM transacoes
ORDER BY valor DESC
LIMIT 2;
```
