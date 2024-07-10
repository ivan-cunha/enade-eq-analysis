# Enade x Student Questionnaire Analysis

## Problem Definition

When I was in college, there were a suspicion from the professors and college administrators that studentes tend to avaluate badly public universities in comparisson to private universities. This would result in the university performing worst in some important indicators (like CPC - Preliminary Course Concept). In this project, I want to investigate if this is true, and if so, in what extent.

## Data

### Enade

The first data source was the Enade Grade of the courses in Brazil, this was available from the government website, [gov.br](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/indicadores-educacionais/indicadores-de-qualidade-da-educacao-superior).  The Enade (National Student Performance Exam) is a mandatory exam for graduating students in various college courses. While the Enade is conducted annually, it does not cover all courses each year. Instead, courses are grouped into categories, and each course participates in the exam periodically. The file contains data of the course and their Enade grade. The Enade grade is not only an indicator by itself, but it is used to calculate other importand indicators as well. Bellow there is a sample of the data.

| Ano  | Código da Área | Área de Avaliação   | Grau Acadêmico | Código da IES | Nome da IES                         | Sigla da IES | Organização Acadêmica | Categoria Administrativa | Código do Curso | Modalidade de Ensino | Código do Município | Município do Curso | Sigla da UF | Nº de Concluintes Inscritos | Nº de Concluintes Participantes | Nota Bruta - FG | Nota Padronizada - FG | Nota Bruta - CE | Nota Padronizada - CE | Conceito Enade (Contínuo) | Conceito Enade (Faixa) | Observação |
| ---- | -------------- | ------------------- | -------------- | ------------- | ----------------------------------- | ------------ | --------------------- | ------------------------ | --------------- | -------------------- | ------------------- | ------------------ | ----------- | --------------------------- | ------------------------------- | --------------- | --------------------- | --------------- | --------------------- | ------------------------- | ---------------------- | ---------- |
| 2022 | 2              | DIREITO             | Bacharelado    | 1             | UNIVERSIDADE FEDERAL DE MATO GROSSO | UFMT         | Universidade          | Pública Federal          | 1               | Educação Presencial  | 5103403             | Cuiabá             | MT          | 91                          | 46                              | 76,33           | 4,686                 | 59,004          | 4,823                 | 4,788                     | 5                      |            |
| 2022 | 13             | CIÊNCIAS ECONÔMICAS | Bacharelado    | 1             | UNIVERSIDADE FEDERAL DE MATO GROSSO | UFMT         | Universidade          | Pública Federal          | 2               | Educação Presencial  | 5103403             | Cuiabá             | MT          | 36                          | 29                              | 60,872          | 2,282                 | 31,11           | 1,603                 | 1,772                     | 2                      |            |
| 2022 | 38             | SERVIÇO SOCIAL      | Bacharelado    | 1             | UNIVERSIDADE FEDERAL DE MATO GROSSO | UFMT         | Universidade          | Pública Federal          | 7               | Educação Presencial  | 5103403             | Cuiabá             | MT          | 57                          | 46                              | 59,419          | 3,163                 | 55,754          | 3,508                 | 3,421                     | 4                      |            |


### Student Questionnaire

The second data source is data from the student questionnaire, available from the Enade Microdata government website [gov.br](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enade).

The student questionnaire is a key component of the Enade exam and is designed to collect detailed information from students about their educational experience. This questionnaire gathers data on various aspects of the students' academic and personal backgrounds, including:

- **Demographic Information:** Age, gender, ethnicity, and socioeconomic status.
- **Educational Background:** Previous academic achievements, reasons for choosing the course, and satisfaction with the educational institution.
- **Course Experience:** Perceptions of the course content, teaching quality, and learning environment.
- **Perceived Skills and Competencies:** Self-assessment of skills and knowledge gained during the course.
- **Future Plans:** Career aspirations, expectations for further education, and employment goals.

The data collected through the student questionnaire provides insights into students' perspectives on their educational experience and helps evaluate the quality of higher education programs in Brazil. This information is used alongside Enade exam scores to assess the effectiveness of academic programs and inform educational policies. We are getting only a subset of this data, questions 27 to 68. These questions are about the **Course Experience**, and is the part that is taken into account when calculating the CPC. These questions are all positive affirmations and the student uses the likert scale (1 - strongly disagree to 6 - strongly agree) to mark his agreement. The numbers 7 and 8 are not an avaluation, they mean "Dont know how to answer" and "Does not apply" respectively . Bellow is a sample of the data

| NU_ANO | CO_CURSO | QE_I27 | QE_I28 | QE_I29 | QE_I30 | QE_I31 | QE_I32 | QE_I33 | QE_I34 | QE_I35 | QE_I36 | QE_I37 | QE_I38 | QE_I39 | QE_I40 | QE_I41 | QE_I42 | QE_I43 | QE_I44 | QE_I45 | QE_I46 | QE_I47 | QE_I48 | QE_I49 | QE_I50 | QE_I51 | QE_I52 | QE_I53 | QE_I54 | QE_I55 | QE_I56 | QE_I57 | QE_I58 | QE_I59 | QE_I60 | QE_I61 | QE_I62 | QE_I63 | QE_I64 | QE_I65 | QE_I66 | QE_I67 | QE_I68 |
| ------ | -------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 2022   | 1115471  | 1      | 2      | 6      | 6      | 6      | 2      | 6      | 6      | 6      | 6      | 6      | 6      | 6      | 5      | 3      | 6      | 5      | 5      | 5      | 8      | 2      | 2      | 6      | 1      | 2      | 4      | 7      | 6      | 6      | 6      | 6      | 6      | 6      | 7      | 6      | 6      | 6      | 6      | 6      | 7      | 7      | 6      |
| 2022   | 67975    | 1      | 2      | 1      | 1      | 3      | 2      | 3      | 2      | 2      | 2      | 2      | 2      | 2      | 1      | 2      | 2      | 4      | 3      | 3      | 2      | 1      | 1      | 2      | 2      | 2      | 1      | 1      | 1      | 2      | 1      | 3      | 2      | 1      | 1      | 1      | 1      | 1      | 2      | 3      | 2      | 4      | 1      |
| 2022   | 54828    | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      |


## ETL and Data Modeling

The ETL was made in Spark ([ETL Notebook](/src/ETL.ipynb)). The data started on S3, then went to Spark inside databricks and the tables were saved for analysis in databricks as well. From the 2 data sources, the database modeling was normalized and at the end resulted in 4 tables. Since the student questionnaire data was in the file per student, an important transformation was to group it by course and get only the mean. The other transformations were explained in the ETL file. Since the precision of the decimal number are known, the columns were modeled as DECIMAL instead of float, to avoid missrounding.

![Database Diagram](/modeling/model.png)

### Curso Table

This table in large but is quite simple, there is some course data, the enade grade and components (general knowledge, specific knowledge and final grade) and the mean of the student questionnaire for each question. The table in databricks is bellow

![Course Table in Databricks](/img/curso_databricks.png)

### IES Table

This table contains the institution data, it was splited from the courses table to avoid inconsistencies. The main column used is the categorie of the institution, Public or Private. 

![IES Table in Databricks](/img/ies_databricks.png)


### Area Table

This table is only the area code and its name. The area is the general area of the courses.

![Area Table in Databricks](/img/area_databricks.png)

### City Table

This table is only the city code and its name

![City Table in Databricks](/img/municipio_databricks.png)


## Analysis

The full analysis and conclusion can be found the the [Analysis Notebook](/src/analysis.ipynb), but in summary, it was found that there is some truth to the suspicion of the professors.