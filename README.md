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
