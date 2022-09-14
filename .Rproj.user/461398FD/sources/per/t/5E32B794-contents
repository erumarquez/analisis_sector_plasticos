
rm(list = ls())

# 01. Carga de bases y paquetes -------------------------------------------

library(googlesheets4)
library(googledrive)
library(tidyverse)
library(clock)
library(writexl)
library(readxl)
library(lubridate)

googledrive::drive_auth("mdointerno@gmail.com")
gs4_auth(token = drive_token())

IPIM <- read_sheet("1ObdXPlbpqM0FUF-P3G7-Vftc6Dkk861sPMZYcysi1MY")
IPIM <- read_sheet("1ObdXPlbpqM0FUF-P3G7-Vftc6Dkk861sPMZYcysi1MY", col_types = paste(replicate(ncol(IPIM), "c"), collapse = ""))  # IPIM
IPI  <- read_sheet("1iMpwsnu4VioJURPICSqdsWbyi4jcEtBzp0CNlBaSpSo")
IPI  <- read_sheet("1iMpwsnu4VioJURPICSqdsWbyi4jcEtBzp0CNlBaSpSo", col_types = paste(replicate(ncol(IPI), "c"), collapse = ""))   # IPI


## me falta hacer la api de precios internacionales 


# 02. Procesamiento ----------------------------------------------------


plasticos_ipim <- IPIM[c(74,83,86),]


plasticos_ipim <- plasticos_ipim %>% gather(., # el . llama a lo que esta atras del %>% 
          key   = Periodo,
          value = Indice,
          3:83)

## Convierto el periodo en date y le acomodo el formato en dia-mes-año   #-------

# plasticos_ipim$Periodo =  as.Date(plasticos_ipim$Periodo, format = "%d-%m-%Y")

plasticos_ipim <- plasticos_ipim %>% 
  arrange(Periodo) %>% 
  select(-nro) %>% 
  spread(. ,
         key   = concepto, #la llave es la variable que va a dar los nombres de columna
         value = Indice) %>% 
  na.omit()


plasticos_ipim$año <- year(dmy(plasticos_ipim$Periodo))

plasticos_ipim <- plasticos_ipim %>% 
  arrange(año) %>% 
  select(-año)


plasticos_ipim$Periodo =  as.Date(plasticos_ipim$Periodo, format = "%d-%m-%Y")


### ya esta la base limpia de ipim






