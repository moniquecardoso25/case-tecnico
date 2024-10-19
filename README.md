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

> Primeiro, é foram criados os 3 schemas para cada hospital dentro da tabela paciente.

```sql
-- Criar o schema stg_hospital_a
CREATE SCHEMA stg_hospital_a;

-- Criar a tabela PACIENTE no schema stg_hospital_a
CREATE TABLE stg_hospital_a.PACIENTE(
    id INT NOT NULL,
    nome VARCHAR(255) NOT NULL,
    dt_nascimento DATE NOT NULL,
    cpf BIGINT NOT NULL,
    nome_mae VARCHAR(255),
    dt_atualizacao TIMESTAMP
);

-- Criar o schema stg_hospital_b
CREATE SCHEMA stg_hospital_b;

-- Criar a tabela PACIENTE no schema stg_hospital_b
CREATE TABLE stg_hospital_b.PACIENTE (
    id INT NOT NULL,
    nome VARCHAR(255) NOT NULL,
    dt_nascimento DATE NOT NULL,
    cpf BIGINT NOT NULL,
    nome_mae VARCHAR(255),
    dt_atualizacao TIMESTAMP
);

-- Criar o schema stg_hospital_c
CREATE SCHEMA stg_hospital_c;

-- Criar a tabela PACIENTE no schema stg_hospital_c
CREATE TABLE stg_hospital_c.PACIENTE (
    id INT NOT NULL,
    nome VARCHAR(255) NOT NULL,
    dt_nascimento DATE NOT NULL,
    cpf BIGINT NOT NULL,
    nome_mae VARCHAR(255),
    dt_atualizacao TIMESTAMP
);

```

> Depois, inseriu-se alguns dados dentro de cada schema, apenas para realizar as consultas. Há nomes duplicados, com mesmo cpf e nome da mãe, que foram inseridos propositalmente para que possam ser removidos durante o problema 3.


```sql

-- Inserir dados no schema stg_hospital_a
INSERT INTO stg_hospital_a.PACIENTE (id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES
(190, 'Maria Clara', '01-04-1991', 11111111111, 'Paula', '27-07-2023 13:40:21'),
(190, 'Maria C.', '01-04-1991', 11111111111, 'Paula', '02-05-2023 18:45:27'),
(365, 'Joao A.', '01-05-1984', 22222222222, 'Pedro', '21-07-2023 14:50:31'),
(365, 'Joao Augusto', '01-05-1984', 22222222222, 'Pedro', '15-01-2023 16:45:22'),
(567, 'Ana Souza', '12-03-1990', 33333333333, 'Lucia', '10-08-2023 10:30:00');


-- Inserir dados no schema stg_hospital_b
INSERT INTO stg_hospital_b.PACIENTE (id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES
(646, 'Carlos Lima', '21-11-1978', 44444444444, 'Mariana', '05-06-2023 11:20:15'),
(646, 'Carlos L.', '21-11-1978', 44444444444, 'Mariana', '28-08-2023 10:00:00'),  
(358, 'Felipe Rocha', '09-09-1983', 66666666666, 'Sofia', '22-04-2023 09:45:35'),
(956, 'Maria Fernanda', '06-09-1991', 77777777777, 'Amanda', '05-05-2023 12:00:00'), 
(140, 'Daniel Costa', '10-06-1992', 88888888888, 'Amanda', '25-05-2023 13:00:00');

-- Inserir dados no schema stg_hospital_c
INSERT INTO stg_hospital_c.PACIENTE (id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
VALUES
(113, 'Larissa Braga', '11-01-1995', 55555555555, 'Fernanda', '05-07-2023 12:45:00'),
(113, 'Larissa B.', '11-01-1995', 55555555555, 'Fernanda', '01-09-2023 08:00:00'), 
(170, 'Pedro Souza', '30-08-1985', 12121212121, 'Marta', '12-06-2023 19:10:00'),
(184, 'Gabriela Mendes', '25-03-1991', 13131313131, 'Valeria', '20-01-2023 10:10:00'),
(155, 'Rafael Lima.', '03-12-1987', 14141414141, 'Claudia', '01-08-2023 15:40:45');

```


## Problema 1

```sql

-- Cria o schema stg_prontuario
CREATE SCHEMA stg_prontuario

-- Cria tabela paciente no schema stg_prontuario
CREATE TABLE stg_prontuario.PACIENTE(

-- Dados dos pacientes
id INT,
nome VARCHAR(255),
dt_nascimento DATE,
cpf BIGINT,
nome_mae VARCHAR(255),
dt_atualizacao TIMESTAMP
);
```


## Problema 2

```sql
INSERT INTO stg_prontuario.PACIENTE (id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao)
SELECT id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao FROM stg_hospital_a.PACIENTE
UNION ALL
SELECT id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao FROM stg_hospital_b.PACIENTE
UNION ALL
SELECT id, nome, dt_nascimento, cpf, nome_mae, dt_atualizacao FROM stg_hospital_c.PACIENTE;
```




## Problema 3
  
## Problema 4

## Problema 5
## Problema 6

## Problema 7
## Problema 8

## Problema 9
## Problema 10
  
  

