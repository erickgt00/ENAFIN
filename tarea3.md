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