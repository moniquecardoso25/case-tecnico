# 
![](https://img.shields.io/badge/feito%20com%20%E2%9D%A4%20por-Monique-Cardoso)
[![LinkedIn Badge](https://img.shields.io/badge/LinkedIn-Profile-informational?style=flat&logo=linkedin&logoColor=white&color=0D76A8)](https://www.linkedin.com/in/monique-cardoso21)


<h1>Resolução de Case</h1>

## Sumário

- [Introdução (Começe por aqui)](#introdução-começe-por-aqui)
- [Problema 1](#problema-1)
- [Problema 2](#problema-2)
- [Problema 3](#problema-3)
- [Problema 4](#problema-4)
- [Problema 5](#problema-5)
- [Problema 6](#problema-6)
- [Problema 7](#problema-7)
- [Problema 8](#problema-8)
- [Problema 9](#problema-9)
- [Problema 10](#problema-10)

## Introdução

### Criação dos schemas para os 3 hospitais.

> Primeiro, foram criados os 3 schemas para cada hospital dentro da tabela paciente.


```sql
-- Criar schema para o hospital A
CREATE SCHEMA stg_hospital_a;

-- Criar tabela no schema stg_hospital_a
CREATE TABLE stg_hospital_a.PACIENTE (
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(255) NOT NULL,
dt_nascimento DATE NOT NULL,
cpf BIGINT NOT NULL,
nome_mae VARCHAR(255),
dt_atualizacao TIMESTAMP,
PRIMARY KEY(id)
);
 
-- Criar schema para o hospital B
CREATE SCHEMA stg_hospital_b;

-- Criar tabela no schema stg_hospital_b
CREATE TABLE stg_hospital_b.PACIENTE(
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(255) NOT NULL,
dt_nascimento DATE NOT NULL,
cpf BIGINT NOT NULL,
nome_mae VARCHAR(255),
dt_atualizacao TIMESTAMP,
PRIMARY KEY(id)
);

-- Criar schema para o hospital C
CREATE SCHEMA stg_hospital_c;

-- Criar tabela no schema stg_hospital_c
CREATE TABLE stg_hospital_c.PACIENTE(
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(255) NOT NULL,
dt_nascimento DATE NOT NULL,
cpf BIGINT NOT NULL,
nome_mae VARCHAR(255),
dt_atualizacao TIMESTAMP,
PRIMARY KEY(id)
);

```

### Schemas criados no MySQL

![image](https://github.com/user-attachments/assets/2a795be6-17f7-423e-a73c-b1ed2977cfbd)


> Depois, inseriu-se alguns dados dentro de cada schema, apenas para realizar as consultas. Há nomes duplicados, com mesmo cpf e nome da mãe, que foram inseridos propositalmente para que possam ser consultados durante os problemas 3 e 4.


```sql

-- Inserir dados no shema stg_hospital_a
INSERT INTO stg_hospital_a.PACIENTE( nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES 
( 'Maria Clara', '1991-04-01', 11111111111, 'Paula', '2023-07-23 13:40:21'), 
( 'Maria C.', '1991-04-01', 11111111111, 'Paula', '2023-07-23 18:45:27'),
( 'Joao A.', '1984-05-01', 22222222222, 'Pedro', '2023-07-21 14:50:31'),
( 'Joao Augusto', '1984-05-01', 22222222222, 'Pedro', '2023-05-21 16:45:22'),
( 'Ana Souza', '1990-03-12', 33333333333, 'Lucia', '2023-08-21 10:30:00');

-- Inserir dados no schema stg_hospital_b
INSERT INTO stg_hospital_b.PACIENTE ( nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES
( 'Carlos Lima', '1978-11-21', 44444444444, 'Mariana', '2023-06-05 11:20:15'),
( 'Carlos L.', '1978-11-21', 44444444444, 'Mariana', '2021-09-05 10:00:00'),  
( 'Felipe Rocha', '1983-09-09', 66666666666, 'Sofia', '2022-07-05 09:45:35'),
( 'Maria Fernanda', '1991-09-06', 77777777777, 'Amanda', '2023-09-026 12:00:00'), 
( 'Daniel Costa', '1995-06-09', 88888888888, 'Amanda', '2023-11-05 13:00:00');

-- Inserir dados no schema stg_hospital_c
INSERT INTO stg_hospital_c.PACIENTE ( nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES
( 'Larissa Braga', '1978-11-21', 55555555555, 'Fernanda', '2023-06-05 12:45:00'),
( 'Larissa B.', '1980-12-21', 55555555555, 'Fernanda', '2023-08-05 08:00:00'), 
( 'Pedro Souza', '1993-08-26', 12121212121, 'Marta', '2023-07-05 19:10:00'),
( 'Gabriela Mendes', '1997-04-12', 13131313131, 'Valeria', '2023-03-05 10:10:00'),
( 'Rafael Lima.', '1995-05-05', 14141414141, 'Claudia', '2023-01-05 15:40:45');

```

### Dados inseridos dentro de cada schema

![image](https://github.com/user-attachments/assets/eb7c6d05-eb49-4b98-b906-becf57fa17d1)


## Problema 1

### Criação do schema prontuáro na tabela paciente

```sql

-- Criar schema prontuário
CREATE SCHEMA stg_prontuario;

-- Criar tabela paciente dentro do schema stg_prontuario
CREATE TABLE stg_prontuario.PACIENTE(

-- Dados dos pacientes
id INT NOT NULL AUTO_INCREMENT,
nome VARCHAR(255) NOT NULL,
dt_nascimento DATE NOT NULL,
cpf BIGINT NOT NULL,
nome_mae VARCHAR(255),
dt_atualizacao TIMESTAMP,
PRIMARY KEY(id)
);
```

### Schema criado

![image](https://github.com/user-attachments/assets/952dba97-97f1-4310-8759-908fa46be24f)


## Problema 2

### Unindo os valores dos schemas no schema stg_prontuario


```sql
-- Insere dados de cada hospital no schema stg_prontuario 
INSERT INTO stg_prontuario.PACIENTE(nome, dt_nascimento, cpf, nome_mae, dt_atualizacao) 
   SELECT nome, dt_nascimento, cpf, nome_mae, dt_atualizacao 
   FROM stg_hospital_a.PACIENTE 
UNION ALL -- Combina os resultados e inclui registros duplicados
   SELECT nome, dt_nascimento, cpf, nome_mae, dt_atualizacao 
   FROM stg_hospital_b.PACIENTE 
UNION ALL 
   SELECT nome, dt_nascimento, cpf, nome_mae, dt_atualizacao 
   FROM stg_hospital_c.PACIENTE;

-- Mostra a tabela
SELECT * FROM stg_prontuario.PACIENTE;

```

### Valores copiados para o schema stg_prontuario 


![image](https://github.com/user-attachments/assets/bf2e3bea-c4ad-4d15-a15a-fcfbffbdb140)


## Problema 3

### Contagem de duplicatas

```sql

SELECT cpf, COUNT(*) AS quantidade
FROM stg_prontuario.PACIENTE
GROUP BY cpf
HAVING COUNT(*) > 1;
```

OU

```sql
SELECT
      cpf, 
      sum(1.0) as quantidade
FROM stg_prontuario.paciente
GROUP BY cpf
HAVING sum(1.0) >= 2;
```

### Quantidade de CPFs duplicados

![image](https://github.com/user-attachments/assets/56ec5286-35a5-46bf-8f8f-a518f2a06619)


## Problema 4

### Data de atualização mais recente do conjunto de pacientes repetidos

```sql

WITH duplicados AS (
    SELECT cpf, MAX(dt_atualizacao) AS max_dt_atualizacao
    FROM stg_prontuario.PACIENTE
    GROUP BY cpf
    HAVING COUNT(*) > 1
)
SELECT p.*
FROM stg_prontuario.PACIENTE p
JOIN duplicados d ON p.cpf = d.cpf AND p.dt_atualizacao = d.max_dt_atualizacao;
```

OU

```sql

WITH a AS (
	 SELECT 
           id,
           nome,
           dt_nascimento,
           cpf,
           nome_mae,
           dt_atualizacao,
           ROW_NUMBER() OVER(PARTITION BY cpf ORDER BY dt_atualizacao desc) AS nr
	 FROM stg_prontuario.paciente
          
)
SELECT id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao
FROM a
WHERE nr = 1
```

### Data de atualização mais recente

![image](https://github.com/user-attachments/assets/fde249e2-3230-4cad-8477-d7f318fdc3e7)


## Problema 5

### Arquivo do VSCode - Jupyter Notebook

### [Link](https://github.com/moniquecardoso25/case-tecnico/blob/57f0b3e37548db5296c9e72a1a739ec81d6f6d90/problema_5.ipynb)


### MySQL

![image](https://github.com/user-attachments/assets/ecd50ac5-741d-42c5-a12f-3fe5aa6a4453)


## Problema 6

## Problema 7
## Problema 8

## Problema 9
## Problema 10
  
  

