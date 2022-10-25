# C-digos-Prof
## Sesion 1-2 R -- 24/10/2022

## 1. Cálculos básicos

### 1.1 Suma
1+1

### 1.2 Calcular el 15% de $1.900
0.15*1900

### 2. Instalar estos Paquetes 
install.packages("tidyverse")
install.packages("dplyr")
install.packages("plyr")
install.packages("tidyr")
install.packages("mlogit")
install.packages("stargazer")
install.packages("rsq")
install.packages("sjPlot")
install.packages("dslabs")

### 2.1 Cargar desde la biblioteca estos Paquetes
library(tidyverse)
library(dplyr)
library(plyr)
library(tidyr)
library(mlogit)
library(stargazer)
library(rsq)
library(sjPlot)
library(dslabs)

## 2. Encuesta CEP
### 2.1 Link: https://www.cepchile.cl/cep/encuestas-cep/encuestas-2010-2021/estudio-nacional-de-opinion-publica-n-85-septiembre-2021

### 2.2 Importar base de datos
library(haven)
base_85 <- read_sav("~/R/R_Projects/Curso-IDEA-2021/encuesta_cep_ago2021/base_85.sav")
View(base_85)

# 2.3Variable numérica
base_85[sapply(base_85, is.numeric)] <- lapply(base_85[sapply(base_85, is.numeric)], as.factor)

## 3. Análisis descriptivo

### 3.1 Frecuencias

### Variable Inicial: elec_pres_1
table(base_85$elec_pres_1)

### Variable dependiente: elec_pres_1 en porcentaje 
table(base_85$elec_pres_1)
table_1 <- table(base_85$elec_pres_1)
prop.table(table_1)


### Ejemplo tablas de contingencia: elec_pres_1 y sexo
sjt.xtab(base_85$elec_pres_1, #filas
         base_85$sexo, #columnas
         file = "1.doc")



## 4. Test de Correlación. Ejemplo
table(base_85$bienestar_2)

sjt.xtab(base_85$bienestar_2, base_85$sexo, file = "4.doc")

cor.test(base_85$sexo, base_85$bienestar_2)

## 5. Recodificar y crear una nueva variable 

## 5.1 Variable dummy 1 candidato
base_85$elec_pres_1.Dummy<-ifelse(base_85$elec_pres_1=="GABRIEL BORIC",1,0)
table(base_85$elec_pres_1.Dummy)

## 5.2 Recodificar variables de preferencias

## Pregunta 14: Interes en la politica
table(base_85$interes_pol_1_b)
base_85$interes_pol_1_b_R = revalue(base_85$interes_pol_1_b, c("1"="2", "2"="2","3"="1", "4"="1", "5"="0", "8"="0","9"="0"))
table(base_85$interes_pol_1_b_R)
