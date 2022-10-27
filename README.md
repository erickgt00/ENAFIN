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

Para esta tarea aplicamos funciones estadisticas con **POSTGRESS*
Una vez cargada nuestra base de datos aplicamos los siguientes resultados:  
#### Calculo de Frecuencia de Empresas por Tamaño
~~~
SELECT tamano, COUNT(*) AS freq
FROM empresa
GROUP BY tamano
ORDER BY freq DESC;
~~~  
~~~
"tamano"	"freq"
"Micro"	147
"Pequeña"	100
"Mediana"	19
"Grande"	14
~~~  

#### Calculo del Estado con mayor cantidad de Empresas (MAXIMO)
~~~
SELECT estado, COUNT(*) AS freq
FROM empresa
GROUP BY estado
ORDER BY freq DESC
LIMIT 1;
~~~  
~~~
"Jalisco"	17
~~~  
#### Calculo del Estado con menor cantidad de Empresas (MINIMO)
~~~
SELECT estado, COUNT(*) AS freq
FROM empresa
GROUP BY estado
ORDER BY freq ASC
LIMIT 1;
~~~  
~~~
"Coahuila"	3
~~~ 

#### Calculo la Moda por Estado
~~~
SELECT mode() 
WITHIN GROUP (ORDER BY estado) AS mode_estado
FROM empresa;
~~~  
~~~
"Distrito Federal"
~~~ 

#### Tabla de Cuartiles para la utilidad de las empresas
~~~
SELECT mode() 
SELECT utilidad,NTILE(4) OVER (PARTITION BY utilidad ORDER BY utilidad) AS Quartile
from profitloss;
~~~ 
~~~
"utilidad"	"quartile"
-110969	1
-109172	1
-78164	1
-59610	1
-42196	1
-40814	1
-34961	1
-34703	1
-34620	1
-34494	1
-33753	1
-33680	1
-33624	1
-33531	1
-33068	1
-33038	1
-32680	1
-31800	1
-31336	1
-31120	1
-30493	1
-28056	1
-27200	1
-25847	1
-25811	1
-25115	1
-24991	1
-24949	1
-24083	1
-23442	1
-21661	1
-21417	1
-20924	1
-20858	1
-20682	1
-20503	1
-19939	1
-19644	1
-19397	1
-19353	1
-19149	1
-18953	1
-18846	1
-18842	1
-18140	1
-18131	1
-18040	1
-17585	1
-17469	1
-17292	1
-17159	1
-17007	1
-17000	1
-16794	1
-16509	1
-16423	1
-16106	1
-16000	1
-15907	1
-15786	1
-15341	1
-15197	1
-14586	1
-14527	1
-14469	1
-14408	1
-14127	1
-13868	1
-13751	1
-13721	1
-13391	1
-12863	1
-12403	1
-12067	1
-12013	1
-11733	1
-11630	1
-11584	1
-11564	1
-11303	1
-10574	1
-10307	1
-10226	1
-10117	1
-10099	1
-9397	1
-9276	1
-8785	1
-8444	1
-8392	1
-8111	1
-7800	1
-7739	1
-7609	1
-7606	1
-7264	1
-6780	1
-6384	1
-6016	1
-6001	1
-5838	1
-5737	1
-5594	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	1
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	2
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	3
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
0	4
15835	1
16546	1
16946	1
17071	1
17300	1
18814	1
19010	1
19384	1
19448	1
19574	1
19729	1
20354	1
20649	1
21135	1
21201	1
21911	1
23056	1
23392	1
23498	1
24779	1
25126	1
25158	1
25646	1
26275	1
26917	1
27001	1
27214	1
27275	1
28191	1
28215	1
28608	1
28680	1
28806	1
30010	1
30560	1
30620	1
31338	1
32173	1
32215	1
32405	1
32427	1
32529	1
32570	1
33210	1
33222	1
33360	1
33660	1
34109	1
35118	1
35308	1
35448	1
35583	1
36151	1
36810	1
36940	1
36956	1
37437	1
37944	1
38534	1
39099	1
39165	1
39504	1
39536	1
39741	1
40799	1
41137	1
41611	1
43039	1
43605	1
45339	1
45590	1
45846	1
46144	1
48513	1
49401	1
49433	1
50075	1
50825	1
51201	1
52082	1
52816	1
53689	1
55036	1
56763	1
57655	1
60623	1
62539	1
63112	1
64294	1
65136	1
65158	1
65433	1
65647	1
66028	1
66357	1
67665	1
68018	1
69066	1
69486	1
70424	1
72475	1
75044	1
75804	1
76920	1
78864	1
79462	1
81799	1
82608	1
109841	1
127630	1
138397	1
144811	1
153076	1
157957	1
158807	1
172101	1
186070	1
205646	1
226417	1
236025	1
262440	1
276123	1
303954	1
324920	1
494598	1
~~~ 




## Conclusiones
El uso de sql es muy util para explorar los datos, sin embargo, para interactuar con los datos para su uso estadistico prefiero usar otros lengaujes como R dado a que estoy mas familiarizado con sus funciones y herramientas estadisticas.
