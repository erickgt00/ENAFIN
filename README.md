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
    z(Micro) --> A
    y(Pequeña) --> A
    x(Mediana)-->A 
    w(Grande)-->A   
    A[Empresa] --> j{Tienen}  
    j{Tienen} --> B[Personal Ocupado]
    j{Tienen} --> B1[Resultados]
    j{Tienen} --> B2[Financiamiento]
    j{Tienen} --> B3[Servicios Fiancieros]
    B --> d1(Dependiente)
    B --> d2(Independiente)
    B1 --> ss1(Ganancias)
    B1 --> ss2(Perdidas)
    B1 --> ss3(Neutras)
    B2 --> f(Utilidades Propoias)
    B2 --> f1(Crédito Aprobado)
    B2 --> f2(Institución)
    B2 --> f3(Motivo)
    B3 --> e(Medios)
    B3 --> e1(Servicios)
    