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


# Tarea 4
## Elegí MySQL (MariaDB) dado que es mas facil seguir las instrucciones a la par que el profesor en clases

# Instrucciones base de datos

CREATE TABLE size_table (
  size_id INT AUTO_INCREMENT PRIMARY KEY,
  size VARCHAR (20)
  );
  
  CREATE TABLE estado (
  estado_id INT AUTO_INCREMENT PRIMARY KEY,
  estado VARCHAR (20)
  );

  CREATE TABLE profitloss (
  ploss_id INT AUTO_INCREMENT PRIMARY KEY,
  ploss VARCHAR (20)
  );
  
  CREATE TABLE tipo_credito (
  c_id INT AUTO_INCREMENT PRIMARY KEY,
  tipo_c VARCHAR (20)
  );

  CREATE TABLE emp_cred (
  empresa_id INT,
  c_id INT
  );

  CREATE TABLE empresa (
  empresa_id INT AUTO_INCREMENT PRIMARY KEY,
  nombre VARCHAR (20),
  size_id INT,
  FOREIGN KEY (size_id) REFERENCES size_table(size_id),
  estado_id INT,
  FOREIGN KEY (estado_id) REFERENCES estado(estado_id),
  ploss_id INT,
  FOREIGN KEY (ploss_id) REFERENCES profitloss(ploss_id),
  c_id INT,
  FOREIGN KEY (c_id) REFERENCES tipo_credito(c_id),
  correo VARCHAR (30)
  
  );

  # Tuve que agregar datos a mis tablas para poder utilizar el modelo e-r como tambien crear nuevas formas de relación entre las mismas
