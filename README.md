ANALISIS EXPLORATORIO DE DATOS (EDA) 

A continuación expongo mi labor realizada sobre los archivos que detallaré, los que se relacionan con el trabajo AIRBNB.
**Archivo 1:** listing.csv
Este archivo contiene la información de los anuncios de Airbnb. Cada fila representa un anuncio.
**Archivo 2:** reviews.csv
Este archivo contiene las reseñas de los anuncios de Airbnb. 
**Archivo 3:** calendar.csv
Este archivo contiene la disponibilidad de los anuncios de Airbnb. 


**Los archivos están disponibles en el siguiente link ** --> https://drive.google.com/drive/u/0/folders/1jMHqEPtrbXW-D8noU5XaOuwu-Bhl3Zvl?hl=es_ES

Inicio con Python, realizando la carga de los archivos para evaluar su contenido, de manera paralela, hago el mismo procedimiento de carga en Power BI.
Esto me permite trabajar a pantalla partida, para conocer el contenido de los archivos, poder filtrar aquellos datos de columnas repetidos, vacíos o no pertinentes al análisis.

import os
import pandas as pd
import csv
os.chdir("2 AirBnB")
Calendario = pd.read_csv("calendar.csv")
Listado = pd.read_csv("listings.csv", low_memory=False)
Resenias = pd.read_csv("reviews.csv")
Columnas_Listado = list(Listado.columns)
print(Columnas_Listado) # Esto imprime un resumen, por lo que la desagrego
Primeras16 = Columnas_Listado[:16]
Segundas16 = Columnas_Listado[16:32]
Terceras16 = Columnas_Listado[32:48]
Cuartas16 = Columnas_Listado[48:64]
Quintas16 = Columnas_Listado[64:80]
Sextas16 = Columnas_Listado[80:96]
Septimas16 = Columnas_Listado[96:]  # Desagregacion de Columnas en listas manejables
for i in Primeras16:
    print(i)  # esto me arroja los datos de las columnas, 
#Realizar la misma tarea con todos los fragmentos de las columnas
#Hecho esto, juntas las impresiones resultantes y observar el listado completo de columnas
#Con este listado en un notebook, se trabaja a pantalla partida con PowerBI 
#En la vista de tablas, en transformar datos, se utilizan los indicadores de composición de columnas
#Con estos datos detallados, se hacen anotaciones sobre el listado de columnas para su filtrado (ej: eliminar aquellas sin datos (vacías))
#Lo mismo anotar tendencias o si se considera importante llamar la atención sobre alguna columna.

#Al notar nombres de columnas con datos curiosos, busqué qué columnas eran por la partición, siendo que estaban dentro de las "Quintas16"

Listado.columns[67:75] #Propongo máscara para investigar las columnas
Filtro = Listado.columns[67:75]
Listado[Filtro] #Los datos arrojados no tienen relevancia para analizar.
# A continuación dejo el listado completo de columnas y mis notas para la transformación en Power BI.

'''
id
url_de_listado
id_de_extracción -----ES UNA SOLA ID , SE ELIMINA
último_extracción -----SOLAMENTE DOS FECHAS , SE ELIMINA
nombre
resumen
espacio
descripción
experiencias_ofrecidas  -- LA COLUMNA NO TIENE DATOS
descripción_general_del_vecindario
notas
tránsito
acceso  --- LA COLUMNA TIENE 43% DE DATOS, DEBERIA SER OBLIGATORIO
interacción
reglas_de_la_casa
url_en_miniatura --- LA COLUMNA NO TIENE DATOS 
url_media ------- LA COLUMNA NO TIENE DATOS
url_de_imagen
url_de_imagen_xl  ------- LA COLUMNA NO TIENE DATOS
id_del_host
url_del_host
nombre_del_host
host_desde
ubicación_del_host
host_sobre
tiempo_de_respuesta_del_host
tasa_de_respuesta_del_host
tasa_de_aceptación_del_host
host_es_superhost
url_en_miniatura_del_host
url_de_imagen_del_host
vecindario_del_host ------ HAY VACIOS, DEBERIA SER OBLIGATORIO
número_de_listados_del_host
total_del_host _listings_count  -- ES REDUNDANTE CON LA COLUMNA ANTERIOR --> ELIMINAR
host_verifications
host_has_profile_pic
host_identity_verified  ---- HAY FALSOS, DEBERIA SER OBLIGATORIO TRUE
street
neighbourhood
neighbourhood_cleansed
neighbourhood_group_cleansed ------- LA COLUMNA NO TIENE DATOS
city
state
zipcode
market
smart_location
country_code
country
latitude
longitude
is_location_exact ---------- TOTALMENTE REDUNDANTE
property_type
room_type
accommodations
bathrooms
rooms
beds
bed_type
amenities
square_feet ------- LA COLUMNA TIENE INFIMOS DATOS
price
weekly_price
monthly_price 
security_deposit
cleaning_fee
guests_included
extra_people
noches_mínimas
noches_máximas
noches_mínimas_mínimas -------REDUNDANCIA -- Luego de analisis, no relevante
noches_mínimas_máximas -------REDUNDANCIA  -- IDEM ANTERIOR DETALLE
noches_máximas_máximas  -------REDUNDANCIA -- IDEM ANTERIOR DETALLE
noches_mínimas_media_ntm -------REDUNDANCIA -- IDEM ANTERIOR DETALLE
noches_máximas_media_ntm -------REDUNDANCIA -- IDEM ANTERIOR DETALLE
calendario_actualizado
tiene_disponibilidad ------cambiaria el true false por yes/no
disponibilidad_30
disponibilidad_60
disponibilidad_90
disponibilidad_365
calendario_última_extracción
número_de_reseñas
número_de_reseñas_ltm -------ver si son especiales (significado ltm = premium?)
primera_reseña  
última_reseña 
puntuación_de_reseñas_calificación
puntuación_de_reseñas_precisión
puntuación_de_reseñas_limpieza
reseña_sc ores_checkin
puntuaciones_de_revisiones_comunicación
puntuaciones_de_revisiones_ubicación
puntuaciones_de_revisiones_valor
requiere_licencia
licencia         -----------LA COLUMNA NO TIENE DATOS
nombres_de_jurisdicciones ----- LA COLUMNA TIENE INFIMOS DATOS
reserva_instantánea
está_listo_para_viajes_de_negocios
política_de_cancelación
requiere_foto_de_perfil_del_huésped
requiere_verificación_telefónica_del_huésped
recuento_calculado_de_anfitriones_
recuento_calculado_de_anfitriones_de_casas_completas
recuento_calculado_de_anfitriones_de_habitaciones_privadas
recuento_calculado_de_anfitriones_de_habitaciones_compartidas
reseñas_por_mes '''


#Del listado resultante, cambiar los tipos de datos para que queden según se indica a continuación (trabajo en Power BI)
# TIPO SEGUN POWER BI
'''
id                              -- int
url_de_listado                  -- text
nombre                          -- text ( CAMBIAR A TITULO)
resumen                         -- text
espacio                         -- text (trataría de hacer que se mida por ambientes, ej 1 ambiente, 2 ambientes, etc)
descripción                     -- text          Cumple función parecida a resumen
descripción_general_del_vecindario  -- text
notas                               -- text      Podría ser suficiente con descripción
tránsito                            -- text
acceso  ---                         -- text       LA COLUMNA TIENE 43% DE DATOS, DEBERIA SER OBLIGATORIO
interacción                     -- text
reglas_de_la_casa               -- text
url_de_imagen                   -- text
id_del_host                     -- text
url_del_host                    -- text
nombre_del_host                 -- text
host_desde                      -- date
ubicación_del_host              -- text
host_sobre                      -- text
tiempo_de_respuesta_del_host    -- text (podría llevarse a tiempos en minutos, usando valores númericos)
tasa_de_respuesta_del_host      -- percentage (primero llevar a 0 los N/A y los vacíos)
tasa_de_aceptación_del_host     -- percentage (primero llevar a 0 los N/A y los vacíos)
host_es_superhost               -- text (reemplazar t --> Yes | f --> No)
url_en_miniatura_del_host       -- text
url_de_imagen_del_host          -- text
vecindario_del_host ------      -- text             HAY VACIOS, DEBERIA SER OBLIGATORIO
número_de_listados_del_host     -- int
total_del_host _listings_count  -- int  
host_verifications              -- text
host_has_profile_pic            -- LA ELIMINO POR FALTA DE RELEVANCIA
host_identity_verified  --      -- text (reemplazar t --> Yes | f --> No)                HAY FALSOS, DEBERIA SER OBLIGATORIO TRUE
street                          -- text
neighbourhood                   -- text
neighbourhood_cleansed          -- text  COMPARAR CON NEIGHBOURHOOD PARA IDENTIFICAR POSIBLE DUPLICIDAD DE DATOS (agregar columna condicional) Se encontraron valores distintos, puede ser por diferente escritura. No investigué más allá
city                            -- text
state                           -- text
zipcode                         -- text 
market                          -- text  DEBERIA SER OBLIGATORIO
smart_location                  -- text
country_code                    -- text
country                         -- text
latitude                        -- int
longitude                       -- int
property_type                   -- text
room_type                       -- text
accommodations                  -- int
bathrooms                       -- int --> HAY QUE CHEQUEAR PORQUE HAY VALORES EXCESIVOS
rooms                           -- int --> CHECK valores 14 y 9 (máximos por posibles outliers)
beds                            -- int
bed_type                        -- text
amenities                       -- text    Punto a mejorar, desglosar en items (ej: wifi, tv, refrigerados, microondas, vista al exterior, gym, etc) permitiría al usuario filtrar por aquellas habitaciones con WIFI incluido por ejemplo
price                           -- decimal fijo (reemplazar "$" por "", para eliminar el signo, comenzar por primero reemplazar "." por "-", para luego reemplazar "." por "," y finalmente reemplazar "-" por "" /vacio/ para poder cambiar a tipo numero)
weekly_price                    -- decimal fijo (trabajo similar a anterior columna, ) 
monthly_price                   -- decimal fijo (trabajo similar a anterior columna, )
security_deposit                -- decimal fijo (trabajo similar a anterior columna, )
cleaning_fee                    -- decimal fijo (trabajo similar a anterior columna, )
guests_included                 -- int
extra_people                    -- decimal fijo (reemplazar "$" por "", para eliminar el signo, comenzar por primero reemplazar "." por "-", para luego reemplazar "." por "," y finalmente reemplazar "-" por "" /vacio/ para poder cambiar a tipo numero)
noches_mínimas                  -- int
noches_máximas                  -- int
calendario_actualizado          -- text
tiene_disponibilidad ------     -- text (Reemplazar t --> Yes | f --> No)            cambiaria el true false por yes/no
disponibilidad_30               -- int
disponibilidad_60               -- int
disponibilidad_90               -- int
disponibilidad_365              -- int
calendario_última_extracción    -- date
número_de_reseñas               -- int
número_de_reseñas_ltm -----     -- int               ver si son especiales (significado ltm = premium?)
primera_reseña                  -- date
última_reseña                   -- date
puntuación_de_reseñas_calificación      --  int
puntuación_de_reseñas_precisión         --  int
puntuación_de_reseñas_limpieza          --  int
reseña_sc ores_checkin                  --  int
puntuaciones_de_revisiones_comunicación --  int
puntuaciones_de_revisiones_ubicación    --  int
puntuaciones_de_revisiones_valor        --  int
requiere_licencia                       --  text (Reemplazar t --> Yes | f --> No) 
reserva_instantánea                     --  text (Reemplazar t --> Yes | f --> No) 
está_listo_para_viajes_de_negocios      --  text (Reemplazar t --> Yes | f --> No) 
política_de_cancelación                 --  text (mejor categorizar para poder analizar preferencias de anfitriones)
requiere_foto_de_perfil_del_huésped     --  text (Reemplazar t --> Yes | f --> No)   
requiere_verificación_telefónica_del_huésped                    --  text (Reemplazar t --> Yes | f --> No) 
recuento_calculado_de_anfitriones_                              --  int
recuento_calculado_de_anfitriones_de_casas_completas            --  int
recuento_calculado_de_anfitriones_de_habitaciones_privadas      --  int
recuento_calculado_de_anfitriones_de_habitaciones_compartidas   --  int
reseñas_por_mes                                                 --  int
'''



#Continuando con la tabla CALENDAR, la misma tiene pocas columnas 
'''
 -- listing_id       -- int  ---->>> CAMPO CLAVE PARA RELACIONAR CON LA TABLA LISTING <<<----
 -- date             -- date
 -- available        -- text (Reemplazar t --> Yes | f --> No)
 -- price            -- decimal fijo  -- decimal fijo (reemplazar "$" por "", para eliminar el signo, comenzar por primero reemplazar "." por "-", para luego reemplazar "." por "," y finalmente reemplazar "-" por "" /vacio/ para poder cambiar a tipo numero) 
 -- adjusted_price   -- decimal fijo  --  ELIMINAR POR REDUNDANCIA --> CHECK QUE  SON LOS MISMOS VALORES QUE LA COLUMNA ANTERIOR
 -- minimum_nights   -- int
 -- maximum_nights   -- int  -- 
'''

#Eso seria todo para la tabla CALENDAR, podría realizarse alguna variante para flexibilizar los datos, pero parece que el par listingId con Date, deben estar en conjunto para ser clave primaria. INVESTIGABLE


#Ahora pasando a la Tabla Reviews para Finalizar el análisis exploratorio de datos (EDA)

'''
-- listing_id    --
-- id            --
-- date          --
-- reviewer_id   --
-- reviewer_name --
-- comments      --
'''

# En principio los tipos de datos están bien y la cantidad de estos está completa.


#Ahora habría que relacionar las tablas

'''

CALENDAR --> DATE + LISTING_ID
REVIEWS --> DATE + LISTING_ID

LISTINGS -->  cambiar nombre ID --> LISTING_ID
