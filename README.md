 Introduccion-a-la-programacion-cientifica
Desarrollo de la actividad grupal de introduccion a la programacion cientifica

# Revisión de las herramientas omicas y bioinformaticas para la prediccion de la resistencia bacteriana de Klebsiella pneumoniae
La resistencia bacteriana es un problema creciente de salud pública, y Klebsiella pneumoniae es una de las bacterias Gram-negativas que ha desarrollado resistencia a múltiples antibióticos, incluyendo los carbapenémicos. Esta situación demanda el desarrollo de herramientas precisas para predecir y monitorear la resistencia bacteriana. Las herramientas ómicas y bioinformáticas han mostrado un gran potencial en este ámbito. QIIME2 (Quantitative Insights Into Microbial Ecology) es una plataforma bioinformática ampliamente utilizada para el análisis de datos de microbioma, que puede adaptarse para investigar la resistencia bacteriana.
## 4. Metodología 

### 4.1 Recolección de Datos 

Bases de Datos: Se recopilarán secuencias genómicas de Klebsiella pneumoniae de bases de datos públicas como NCBI, PATRIC y ResFinder. 

Metadatos: Se incluirán datos sobre el origen de las muestras, fenotipos de resistencia y métodos de aislamiento. 

4.2 Análisis con QIIME2 

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
 
