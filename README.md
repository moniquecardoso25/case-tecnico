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

> O schema prontuário foi criado conforme a definição requerida no desafio técnico. No CPF foi usado o tipo de dado BIGINT porque o mesmo tem 11 caracteres e o INT aceita apenas até 10 caracteres. O auto_increment é usado para gerar um ID automaticamente quando um novo registro é inserido na tabela. O ID é único para cada paciente, por isso foi utilizada a chave primária (primary key). 

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

> Os valores dos 3 schemas foram copiados para a nova tabela PACIENTE criada no schema stg_prontuario. Essa união se dá por meio do UNION ALL, que foi utilizado para incluir os valores duplicados, que serão utilizados nos problemas 3 e 4. Após isso, fez-se uma consulta da tabela através do comando SELECT a fim de verificar os valores desse novo schema criado.

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

> O código abaixo retorna a quantidade de pacientes duplicados por meio da contagem COUNT() de seus CPFs que aparecem mais de uma vez (HAVING COUNT(*)>1) na tabela.

### Contagem de duplicatas


```sql
-- Contar a quantidade de cpfs duplicados
SELECT cpf, COUNT(*) AS quantidade
FROM stg_prontuario.PACIENTE
GROUP BY cpf
HAVING COUNT(*) > 1;
```


### Quantidade de CPFs duplicados

![image](https://github.com/user-attachments/assets/56ec5286-35a5-46bf-8f8f-a518f2a06619)


## Problema 4

> O código identifica CPFs duplicados na tabela de pacientes, retornando os registros com a data de atualização mais recente para cada CPF duplicado.

### Data de atualização mais recente do conjunto de pacientes repetidos

```sql
-- Mostrar a data de atualização mais recente dos cpfs duplicados
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


### Data de atualização mais recente

![image](https://github.com/user-attachments/assets/fde249e2-3230-4cad-8477-d7f318fdc3e7)


## Problema 5

> Foi utilizado a extensão do Jupyter no VSCode. Acesse os códigos no link abaixo.
> Os arquivos foram lidos em modo leitura ('r) e depois foram feitas as partições para cada coluna das 6 tabelas. Em que as strings foram divididas em partes menores, de acordo com os dados informados nos arquivos com final "_layout".
> A conexão com o banco de dados MySQL foi realizada no schema stg_prontuario.
> As queries foram criadas, ou seja as tabelas com os nomes, tipos e tamanhos das colunas de cada arquivo e os dados inseridos no banco de dados.

### [Jupyter Notebook](https://github.com/moniquecardoso25/case-tecnico/blob/d535d8eb605eceb5ff8dc1d500b38a11936290ad/problema_5.ipynb)

> Os dados dos arquivos foram inseridos no MySQL via Python, conforme mostra as imagens imagens abaixo: 


![image](https://github.com/user-attachments/assets/f6256a0d-0e72-4414-97c6-e680dda92d39)


![image](https://github.com/user-attachments/assets/8e29aad8-f477-4507-80bf-7fd7a7517c64)


![image](https://github.com/user-attachments/assets/1242fc8a-46cd-44e5-a53f-355bed8f38a3)


## Problema 6

> Aravés desse [Link](https://open-meteo.com/en/docs#latitude=-22.9064&longitude=-43.1822&hourly=pressure_msl&timezone=America%2FSao_Paulo), no campo API Response (Python), foi gerada a API da pressão atmosférica da cidade do Rio de Janeiro. O site cria um código padrão informando a latitude e longitude da cidade pesquisada em sua busca principal, onde foi possível obter a tabela com os dados da previsão da pressão atmosférica dos próximos 7 dias (21 até 27 de Outubro de 2024). Depois, os dados foram inseridos no MySQL.

### [Código do Python](https://github.com/moniquecardoso25/case-tecnico/blob/fbcf724b9e3824d39601c8196b4e0413fce3dc8e/Problema_6.ipynb)

Pressão Atmosférica extraída via API com Python. Dados inseridos no MySQL.

![image](https://github.com/user-attachments/assets/c705c774-7254-4e1b-a295-c9fb6d3ecde3)


## Problema 7

> O código SQL criou de uma nova tabela num esquema chamado stg_prontuario, denominada atendimento_prescricao. Essa tabela tem como objetivo estabelecer um relacionamento entre duas entidades: atendimentos e prescrições médicas, através de uma chave estrangeira do id dos atendimentos (id_atend).

### Tabela Atendimento

![image](https://github.com/user-attachments/assets/765d5729-916b-4712-8f06-52bd8a97d036)


### Tabela Prescrição

![image](https://github.com/user-attachments/assets/cb5db923-b0d7-4b88-9e39-559d21c03918)


## Problema 8

> Os valores informados no desafio foram inseridos na tabela para calcular a quantidade média de medicamentos prescritos dos atendimentos tipo U (Urgência).
> Os tipos dos atendimentos também foram inseridos nos valores.

### Inserção de valores nas tabelas

![image](https://github.com/user-attachments/assets/55f76f2a-acfe-441b-b833-b5bc438dabbd)


### Consulta dos valores da tabela ATENDIMENTO

![image](https://github.com/user-attachments/assets/f620af31-a2f4-4486-bacc-eb24e051f5c6)


### Consulta dos valores da tabela ATENDIMENTO_PRESCRIÇÃO

![image](https://github.com/user-attachments/assets/6874b1b6-2567-41bf-b35c-148922ad4257)


### Cálculo da média

![image](https://github.com/user-attachments/assets/0ad119c1-cd5a-4830-9fd3-edbe6e99c002)


## Problema 9

> O código Python apresentado verifica se todos os medicamentos de uma prescrição estão disponíveis em um estoque. Os medicamentos são representados por letras conforme pedido no desafio. 
> No print(verificar_prescricao("a", "b")), retorna False porque o medicamento "a" não está no estoque. Já no
print(verificar_prescricao("aa", "aab")), retorna True porque há quantidade suficiente de "a" no estoque para atender à prescrição

### [Código do Python](https://github.com/moniquecardoso25/case-tecnico/blob/cdf451ed072be6e3d88c090212a676c60e665246/problema_9.ipynb)


## Problema 10

> Datas aleatórias foram criadas apenas para gerar o gráfico de barra(utilizando a biblioteca Matplotlib). As datas descritas numa lista foram inseridas em Series do Pandas, que é o mais viável nesse caso, pois há apenas 1 coluna na tabela. O gráfico mostra a quantidade de atendimentos médicos por dia, através da contagem das datas.

### [Código do Python](https://github.com/moniquecardoso25/case-tecnico/blob/0b2a389711c019e0620563382108ee02d4cb229a/problema10%20(1).ipynb)  
  

