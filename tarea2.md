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