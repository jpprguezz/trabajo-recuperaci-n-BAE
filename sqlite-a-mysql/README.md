Para poder empezar este trabajo, debemos migrar las tablas que utilizamos en el proyecto desde sqlite a mysql:


- #### Tabla "profesores"
```sql
CREATE TABLE profesores (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Apellidos VARCHAR(100) NOT NULL,
    Nombre VARCHAR(100) NOT NULL,
    DNI VARCHAR(100),
    Es_Tutor ENUM('Si', 'No')
);

INSERT INTO profesores (Apellidos, Nombre, DNI, Es_Tutor) VALUES ('García', 'Juan', '12345678A', 'Si');
INSERT INTO profesores (Apellidos, Nombre, DNI, Es_Tutor) VALUES ('López', 'María', '87654321B', 'No');
INSERT INTO profesores (Apellidos, Nombre, DNI, Es_Tutor) VALUES ('Martínez', 'Carlos', NULL, 'Si');
```

- #### Tabla "tiene"
```sql
CREATE TABLE tienen_a_profesores (
    ID_Profesores INT,
    DNI_Estudiante VARCHAR(100),
    FOREIGN KEY (ID_Profesores) REFERENCES direccion(ID),
    FOREIGN KEY (DNI_Estudiante) REFERENCES estudiantes(DNI)
);

INSERT INTO tienen_a_profesores (ID_Profesores, DNI_Estudiante) VALUES
(1, '12345678A'),
(2, '87654321B'),
(3, '11223344C');
```

- #### Tabla "estudiantes"

```sql
CREATE TABLE estudiantes (
    DNI VARCHAR(100) NOT NULL PRIMARY KEY,
    Nombre_Estudiante VARCHAR(100) NOT NULL,
    Apellidos_Estudiante VARCHAR(100) NOT NULL
);

INSERT INTO Estudiantes (DNI, Nombre_Estudiante, Apellidos_Estudiante) VALUES
('12345678A', 'Juan', 'García'),
('87654321B', 'María', 'López'),
('11223344C', 'Carlos', 'Martínez');
```

- #### Tabla "pertenencia_a_estudiantes"

```sql
CREATE TABLE pertenencia_a_estudiantes (
    ID_Email INT, 
    DNI_Estudiante VARCHAR(100), 
    FOREIGN KEY (ID_Email) REFERENCES email(ID),
    FOREIGN KEY (DNI_Estudiante) REFERENCES estudiantes(DNI)
);

INSERT INTO pertenencia_a_estudiantes (ID_Email, DNI_Estudiante) VALUES
(1, '12345678A'),
(2, '87654321B'),
(3, '11223344C');
```

- #### Tabla "email"

```sql
CREATE TABLE email (
    ID INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    email VARCHAR(100) NOT NULL
);

INSERT INTO email (email) VALUES
('ejemplo1@gmail.com'),
('ejemplo2@gmail.com'),
('ejemplo3@gmail.com');
```

- ### Tabla "posee"

```sql
CREATE TABLE posee_estudiantes (
    ID_Direccion INT,
    DNI_Estudiante VARCHAR(100),
    FOREIGN KEY (ID_Direccion) REFERENCES direccion(ID),
    FOREIGN KEY (DNI_Estudiante) REFERENCES estudiantes(DNI)
);

INSERT INTO posee_estudiantes (ID_Direccion, DNI_Estudiante) VALUES
(1, '12345678A'),
(2, '87654321B'),
(3, '11223344C');
```


- ### Tabla "direccion"

```sql
CREATE TABLE direccion (
	ID  INT NOT NULL PRIMARY KEY,
	Provincia VARCHAR(100) NOT NULL,
	Numero INT NOT NULL,
	Codigo_Postal INTEGER NOT NULL,
	Piso INT NOT NULL,
	Calle VARCHAR(100) NOT NULL,
	Municipio VARCHAR(100) NOT NULL
 );

INSERT INTO Direccion (ID, Provincia, Numero, Codigo_Postal, Piso, Calle, Municipio) VALUES
(1, 'Madrid', 123, 28001, 1, 'Calle Viena', 'Madrid'),
(2, 'Barcelona', 456, 08001, 2, 'Calle Segovia', 'Barcelona'),
(3, 'Valencia', 789, 46001, 3, 'Calle Arcilleria', 'Valencia');
```
