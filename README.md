# ENAFIN
Proyecto de ENAFIN 2022

# Proyecto Base de Datos Relacionales
# Descripcion de BD seleccionada
    # Para este proyecto se utilizará la base de datos del INEGI
    # ENAFIN 2019 la cual tiene como objetivo recabar información
    # estadística que permita identificar las necesidades, fuentes y
    # condiciones de acceso al financiamiento de las empresas privadas no
    # financieras de México, así como el uso del financiamiento y
    # los servicios financieros

# Descripción de los datos
    ### La población objetivo son las Empresas del país con 6 o mas 
    ### personas ocupadas

# Realización de Modelo E-R
graph TD
    o1{{Num}} --> z(Micro) --> A 
    o2{{Num}} --> y(Pequeña) --> A
    o3{{Num}} --> x(Mediana)-->A 
    o4{{Num}} --> w(Grande)-->A   
    A[Empresa] --> j{Tienen} 
    j{Tienen} --> B[Personal Ocupado]
    j{Tienen} --> B1[Resultados]
    j{Tienen} --> B2[Financiamiento]
    j{Tienen} --> B3[Servicios Fiancieros]
    B --> d1(Dependiente)--> o6{{Num}}
    B --> d2(Independiente)--> o7{{Num}}
    B1 --> ss1(Ganancias)--> o8{{Num}}
    B1 --> ss2(Perdidas)--> o9{{Num}}
    B1 --> ss3(Neutras)--> o10{{Num}}
    B2 --> f(Utilidades Propoias)--> o11{{Num}}
    B2 --> f1(Crédito Aprobado)--> o12{{Num}}
    B2 --> f2(Institución)--> o13{{Num}}
    B2 --> f3(Motivo) --> o14{{Num}}
    B3 --> e(Medios)--> o15{{Num}}
    B3 --> e1(Servicios) --> o16{{Num}}

# Esquema Modelo E-R

    empresa (_id_, micro, pequeña, mediana, grande)

    Personal_Ocupado (_id_, dependiente, independiente)

    Resultados (_id_, ganancias, perdidas, neutras)

    Financiamiento (_id_ u.propias, credito.apr, institucion, motivo)

    Serv.Financieros (_id_, medios, servicios)

# Diagrama E-R
erDiagram
Empresa ||--}o Personal_Ocupado : ""
Empresa ||--}o Resultados : ""
Empresa ||--}o Financiamiento : ""
Empresa ||--}o Serv_Financieros : ""

 Empresa {
    Num Micro
    Num Pequena
    Num Mediana
    Num Grande

  }
  Resultados {
    Num Ganancias
    Num Perdidas
    Num Neutros
  }

  Personal_Ocupado {
    Num Dependiente
    Num Independiente
  }

Financiamiento {
    Num u_propias
    Num credito_aprob
    Num institucion
    Num motivo
  }

Serv_Financieros {
    Num medios
    Num servicios

  }


# Algebra Relacional

    Empresas Micro con Ganancias en sus Resultados:
Πid.micro[σganancias=micro(Resultados)]

Personal Ocupado en Empresas Grandes
Πid.grande[σdependiente∪independiente=grande(Personal_Ocupado )]

Tipo de Financiamiento de Empresas Pequeñas
Πid.pequeñas[σu.propias∪credito.apr∪institucion∪motivo=pequeña(Fiananciamiento)]

Total de Créditos Aprobados
Πid.credito.apr[σmicro∪pequeña∪mediana∪grande(Financiamiento)]


## Tarea de Consulta 
### Erick Adrian Garza Tamez

Para esta tarea aplicamos funciones estadisticas con **lenguaje R**
Una vez cargada nuestra base de datos aplicamos los siguientes resultados:  
#### Calculo de Frecuencia de Empresas por Estado
~~~
emp_nl <- as.data.frame(table(general$ubicación))
print(emp_nl)
~~~  
~~~
> print(emp_nl)
                  Var1 Freq
1       Aguascalientes    8
2      Baja California    8
3  Baja California Sur    9
4             Campeche   10
5              Chiapas    9
6            Chihuahua   16
7             Coahuila    3
8               Colima    7
9     Distrito Federal   17
10             Durango    6
11          Guanajuato    7
12            Guerrero    6
13             Hidalgo   10
14             Jalisco   17
15              México    8
16           Michoacán    8
17             Morelos    6
18             Nayarit    8
19          Nuevo León    8
20              Oaxaca   10
21              Puebla    5
22           Querétaro    5
23        Quintana Roo    9
24     San Luis Potosí   10
25             Sinaloa    9
26              Sonora   12
27             Tabasco    9
28          Tamaulipas    5
29            Tlaxcala   10
30            Veracruz   11
31             Yucatán    5
32           Zacatecas    9
~~~  

#### Calculo de caracteres minimos y maximos de los nombres de las empresas como tambien la mediana y cuantiles
~~~
x <- c(general$nombre)
nombres <- (str_length(x))
summary(nombres)
~~~  
~~~
Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
    7.0    12.0    15.5    15.7    20.0    20.0 
~~~  
#### Calculo de la moda de los Estados de las Empresas
~~~
mfv(general$ubicación)
~~~  
~~~
"Distrito Federal" "Jalisco" 
~~~  

## Conclusiones
He tenido problemas con mysql por lo que ocuidi al lenguaje de progración R, aun asi tuve que descargar librerias que desconocía como las que utilice para sacar la moda, sin duda es una gran herramienta estadistica que me gustaría seguir usando