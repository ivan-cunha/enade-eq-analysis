# Enade x Student Questionnaire Analysis

## Problem Definition

During my time in college, there was a suspicion among professors and administrators that students tend to rate public universities more poorly compared to private institutions. This perception might affect important indicators, such as the CPC (Preliminary Course Concept). This project aims to investigate whether this suspicion holds true and, if so, to what extent it impacts these indicators.

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

We focus on a subset of this data — questions 27 to 68 — which pertain to Course Experience and are used in calculating the CPC. These questions consist of positive statements rated on a Likert scale from 1 (strongly disagree) to 6 (strongly agree). The numbers 7 and 8 are reserved for "Don't know how to answer" and "Does not apply," respectively. Below is a sample of the data:

| NU_ANO | CO_CURSO | QE_I27 | QE_I28 | QE_I29 | QE_I30 | QE_I31 | QE_I32 | QE_I33 | QE_I34 | QE_I35 | QE_I36 | QE_I37 | QE_I38 | QE_I39 | QE_I40 | QE_I41 | QE_I42 | QE_I43 | QE_I44 | QE_I45 | QE_I46 | QE_I47 | QE_I48 | QE_I49 | QE_I50 | QE_I51 | QE_I52 | QE_I53 | QE_I54 | QE_I55 | QE_I56 | QE_I57 | QE_I58 | QE_I59 | QE_I60 | QE_I61 | QE_I62 | QE_I63 | QE_I64 | QE_I65 | QE_I66 | QE_I67 | QE_I68 |
| ------ | -------- | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| 2022   | 1115471  | 1      | 2      | 6      | 6      | 6      | 2      | 6      | 6      | 6      | 6      | 6      | 6      | 6      | 5      | 3      | 6      | 5      | 5      | 5      | 8      | 2      | 2      | 6      | 1      | 2      | 4      | 7      | 6      | 6      | 6      | 6      | 6      | 6      | 7      | 6      | 6      | 6      | 6      | 6      | 7      | 7      | 6      |
| 2022   | 67975    | 1      | 2      | 1      | 1      | 3      | 2      | 3      | 2      | 2      | 2      | 2      | 2      | 2      | 1      | 2      | 2      | 4      | 3      | 3      | 2      | 1      | 1      | 2      | 2      | 2      | 1      | 1      | 1      | 2      | 1      | 3      | 2      | 1      | 1      | 1      | 1      | 1      | 2      | 3      | 2      | 4      | 1      |
| 2022   | 54828    | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      | 1      |


## ETL and Data Modeling

The ETL was made in Spark ([ETL Notebook](/src/ETL.ipynb)). The data was initially stored on S3, then processed in Spark within Databricks, and finally saved as tables for analysis. The database was normalized from the two data sources, resulting in four tables. One key transformation involved aggregating the student questionnaire data by course to calculate the mean responses for each question, as explained in the ETL notebook. Additionally, to avoid rounding issues, the columns were modeled as DECIMAL instead of FLOAT.

![Database Diagram](/modeling/model.png)

### Curso Table

This table is comprehensive, containing course data, Enade grades, components (general knowledge, specific knowledge, and final grade), and the average responses from the student questionnaire for each question.

![Course Table in Databricks](/img/curso_databricks.png)

### IES Table

This table holds data about educational institutions, separated from the courses table to prevent inconsistencies. The primary focus is on the institution's category: Public or Private.

![IES Table in Databricks](/img/ies_databricks.png)


### Area Table

This table includes the area code and its name, representing the general academic field of the courses.

![Area Table in Databricks](/img/area_databricks.png)

### City Table

This table lists city codes and names.

![City Table in Databricks](/img/municipio_databricks.png)


## Analysis

For a detailed analysis and conclusions, refer to the [Analysis Notebook](/src/analysis.ipynb). In summary, the findings suggest that there is some validity to the professors' suspicions about students' evaluations of public versus private universities.

## Conclusion

### Achievements and Challenges

In this project, we aimed to investigate whether there is a tendency for students to rate public universities lower than private ones, and to what extent this affects key indicators like the CPC (Preliminary Course Concept). We successfully demonstrated that there is indeed some validity to the professors' suspicion that public universities may receive lower evaluations compared to private institutions. The analysis was supported by combining Enade grades with student questionnaire data, providing a comprehensive view of students' perceptions.

One of the main challenges we encountered was constructing a robust database model and developing effective queries for analysis. This process required careful design and iterative refinement to ensure the accuracy and relevance of the data used in our evaluation.

### Future Work

For future work, we plan to extend the analysis to include data from additional years beyond 2022 to identify trends over time. We will also focus on evaluating the CPC indicator to understand its relationship with the data collected from the student questionnaire. These steps will help to provide a more complete picture of the quality of higher education in Brazil and offer deeper insights into the factors influencing students' perceptions.