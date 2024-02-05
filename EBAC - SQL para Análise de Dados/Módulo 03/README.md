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

#### [**2.1. Query 1**]()
```sql
SELECT *
FROM transacoes
```

#### [**2.2. Query 2**]()
```sql
SELECT id_cliente,
	valor,
	id_loja AS nome_loja
FROM transacoes;
```

#### [**2.3. Query 3**]()
```sql
SELECT DISTINCT id_loja AS nome_loja
FROM transacoes;
```

### **3. Ordenando e limitando dados**

#### [**3.1. Query 4**]()
```sql
SELECT id_cliente,
	valor
FROM transacoes
ORDER BY valor DESC
LIMIT 2;
```
