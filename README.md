**María Isabel García Sejas**, **Astrid LIliana Vargas Sanchez**

Desarrollo de la actividad grupal de introducción a la programación cientifica: "Crear un repositorio github. Control de versiones"

![Imagen en 3D de KP](Imagen/Klebsiella.jpg)

# Revisión de las herramientas omicas y bioinformaticas para la prediccion de la resistencia bacteriana de *Klebsiella pneumoniae*

La resistencia bacteriana representa un desafio significativo en la salud pública, particularmente en entornos hospitalarios. *Klebsiella pneumoniae* es una de las bacterias Gram-negativas que ha desarrollado resistencia a múltiples antibióticos, incluyendo los carbapenémicos. Esta resistencia complica el tratamiento de infecciones que afectan diversas partes del cuerpo, desde el tracto urinario hasta los pulmones y tejidos blandos. Esta situación demanda el desarrollo de herramientas precisas para predecir y monitorear la resistencia bacteriana. Las herramientas ómicas y bioinformáticas han mostrado un gran potencial en este ámbito. QIIME2 (Quantitative Insights Into Microbial Ecology) es una plataforma bioinformática ampliamente utilizada para el análisis de datos de microbioma, que puede adaptarse para investigar la resistencia bacteriana.

## Hipotesis 

El uso de herramientas ómicas y bioinformáticas, específicamente QIIME2, permite una predicción precisa y eficaz de la resistencia bacteriana en *Klebsiella pneumoniae*, facilitando la identificación de genes de resistencia y la correlación con metadatos clínicos y epidemiológicos. 

## 2. Objetivo General 

- Revisar y evaluar las herramientas ómicas y bioinformáticas disponibles para la predicción de la resistencia bacteriana en *Klebsiella pneumoniae*, utilizando QIIME2 como plataforma de análisis. 

## 2.1 Objetivos especificos  

- Compilar un Conjunto de datos Integral de Secuencias Genómicas y Metadatos de *Klebsiella pneumoniae*: 

- Implementar la Plataforma QIIME2 para el Análisis de Secuencias Genómicas 

- Evaluar la Calidad de las Secuencias y Realizar el Filtrado de Datos mediante QIIME2 

- Identificar y clasificar genes de resistencia antibiótica presentes en las secuencias genómicas utilizando métodos de clasificación disponibles en QIIME2 

## 3. Justificación 
La resistencia bacteriana de *Klebsiella pneumoniae* representa una amenaza significativa para la salud global. La integración de herramientas ómicas y bioinformáticas, como QIIME2, puede proporcionar un enfoque holístico para la predicción y monitoreo de la resistencia, facilitando la implementación de estrategias más efectivas de control y tratamiento. 

## 4. Metodología 

### 4.1 Recolección de Datos 

**Bases de Datos:** Se recopilarán secuencias genómicas de *Klebsiella pneumoniae* de bases de datos públicas como NCBI, PATRIC y ResFinder. 

**Metadatos:** Se incluirán datos sobre el origen de las muestras, fenotipos de resistencia y métodos de aislamiento. 

### 4.2 Análisis con QIIME2 

Instalación y Configuración de QIIME2: Instalación de QIIME2 en un entorno Conda y configuración para análisis. 

bash 

Copiar código 

conda create -n qiime2-2024.2 --file https://data.qiime2.org/distro/core/qiime2-2024.2-py38-osx-conda.yml 
conda activate qiime2-2024.2 
 

Importación de Datos: Importación de secuencias genómicas en QIIME2. 

bash 

Copiar código 

qiime tools import \ 
  --type 'SampleData[PairedEndSequencesWithQuality]' \ 
  --input-path emp-paired-end-sequences \ 
  --output-path demux-paired-end.qza 
 

Calidad de Datos y Filtrado: Evaluación de la calidad de las secuencias y filtrado de datos de baja calidad. 

bash 

Copiar código 

qiime demux summarize \ 
  --i-data demux-paired-end.qza \ 
  --o-visualization demux-paired-end.qzv 
 

Análisis de la Diversidad: Evaluación de la diversidad microbiana y la resistencia utilizando métricas de diversidad alfa y beta. 

bash 

Copiar código 

qiime diversity core-metrics-phylogenetic \ 
  --i-phylogeny rooted-tree.qza \ 
  --i-table table.qza \ 
  --p-sampling-depth 1103 \ 
  --m-metadata-file sample-metadata.tsv \ 
  --output-dir core-metrics-results 
 

Análisis de Resistencia: Utilización de herramientas específicas dentro de QIIME2 para la identificación de genes de resistencia antibiótica. 

bash 

Copiar código 

qiime feature-classifier classify-sklearn \ 
  --i-classifier classifier.qza \ 
  --i-reads rep-seqs.qza \ 
  --o-classification taxonomy.qza 
## 5. Resultados Esperados 

Identificación de genes de resistencia predominantes en *Klebsiella pneumoniae*. 

Evaluación de la efectividad de QIIME2 en la predicción de la resistencia bacteriana. 

Recomendaciones para la implementación de herramientas ómicas y bioinformáticas en la vigilancia de la resistencia bacteriana. 

## 6. Conclusión 

Este estudio proporcionará una revisión integral de las herramientas ómicas y bioinformáticas disponibles para predecir la resistencia bacteriana en *Klebsiella pneumoniae*, destacando el potencial de QIIME2 como una plataforma versátil para el análisis de datos de microbioma en este contexto. 

## 7. Bibliografia

1. Rubio A, Jimenez J, Pérez-Pulido AJ. Assessment of selection pressure exerted on genes from complete pangenomes helps to improve the accuracy in the prediction of new genes. Brief Bioinform. 2022 Feb 2;. doi: 10.1093/bib/bbac010
2. Xu, L., Sun, X., & Ma, X. (2017). Systematic review and meta-analysis of mortality of 
patients infected with carbapenem-resistant Klebsiella pneumoniae. Annals of 
Clinical Microbiology and Antimicrobials, 16(1), 18. 
https://doi.org/10.1186/s12941-017-0191-3 .
3. Hernández Marta, Quijada Narciso M., Lázaro David Rodríguez, Eiros José María. Aplicación de la secuenciación masiva y la bioinformática al diagnóstico microbiológico clínico. Rev. argent. microbiol.  [Internet]. 2020  Jun [citado  2024  Jun  17] ;  52( 2 ): 101-110. Disponible en: http://www.scielo.org.ar/scielo.php?script=sci_arttext&pid=S0325-75412020000200101&lng=es.  http://dx.doi.org/10.1016/j.ram.2019.06.003.
4. Bokulich, N. A., Kaehler, B. D., Rideout, J. R., Dillon, M., Bolyen, E., Knight, R., … Gregory Caporaso, J. (2018). Optimizing taxonomic classification of marker-gene amplicon sequences with QIIME 2’s q2-feature-classifier plugin. Microbiome, 6(1), 90. https://doi.org/10.1186/s40168-018-0470-z
5. Echeverri Toro Lina María, Cataño Correa Juan Carlos. Klebsiella pneumoniae como patógeno intrahospitalario: epidemiología y resistencia. Iatreia  [Internet]. 2010  Sep [cited  2024  June  17] ;  23( 3 ): 240-249. Available from: http://www.scielo.org.co/scielo.php?script=sci_arttext&pid=S0121-07932010000300006&lng=en.

