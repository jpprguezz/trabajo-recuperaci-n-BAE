## Procedimientos

1. Insertar nuevos profesores en la tabla profesores

```sql
DELIMITER //
CREATE PROCEDURE InsertarNuevoProfesor(in iterations INT)
BEGIN
    DECLARE counter INT DEFAULT 0;
    DECLARE p_apellidos VARCHAR(100);
    DECLARE p_nombre VARCHAR(100);
    DECLARE p_DNI VARCHAR(100);
    DECLARE p_es_tutor ENUM('Si', 'No');
    DECLARE aux INT;
    WHILE counter < iterations DO
    SET p_apellidos = CONCAT('Profesor', ROUND(RAND() * 10000));
    SET p_nombre = CONCAT('Nombre', ROUND(RAND() * 10000));
    SET p_DNI = FLOOR(RAND() * 99999999);
    SET aux = floor(RAND() * 2);
    SET p_es_tutor = IF(aux = 0, 'Si', 'No');

    INSERT INTO profesores (Apellidos, Nombre, DNI, Es_Tutor) VALUES (p_apellidos, p_nombre, p_DNI, p_es_tutor);
    SET counter = counter  + 1;
    END WHILE;
END//
DELIMITER ;

CALL InsertarNuevoProfesor(16)

SELECT * FROM profesores;
+----+--------------+------------+-----------+----------+
| ID | Apellidos    | Nombre     | DNI       | Es_Tutor |
+----+--------------+------------+-----------+----------+
|  1 | García       | Juan       | 12345678A | Si       |
|  2 | López        | María      | 87654321B | No       |
|  3 | Martínez     | Carlos     | NULL      | Si       |
|  4 | Profesor1897 | Nombre2302 | 58183837  | Si       |
|  5 | Profesor3478 | Nombre830  | 37164252  | No       |
|  6 | Profesor9310 | Nombre8275 | 34448738  | Si       |
|  7 | Profesor1661 | Nombre1109 | 5613668   | No       |
|  8 | Profesor5714 | Nombre131  | 35141182  | No       |
|  9 | Profesor5342 | Nombre5180 | 98719377  | Si       |
| 10 | Profesor9488 | Nombre5979 | 14311839  | No       |
| 11 | Profesor1797 | Nombre1332 | 12692235  | Si       |
| 12 | Profesor7939 | Nombre2647 | 94178644  | No       |
| 13 | Profesor7488 | Nombre9997 | 75204978  | No       |
| 14 | Profesor5493 | Nombre4633 | 66838455  | No       |
| 15 | Profesor7555 | Nombre9213 | 33987918  | No       |
| 16 | Profesor6578 | Nombre4826 | 43942168  | No       |
| 17 | Profesor4287 | Nombre8955 | 19143164  | Si       |
| 18 | Profesor7785 | Nombre807  | 6790650   | Si       |
| 19 | Profesor2841 | Nombre1276 | 78597724  | No       |
+----+--------------+------------+-----------+----------+
```

2. Insertar nuevos estudiantes en la tabla estudiantes

```sql
DELIMITER //
CREATE PROCEDURE InsertarNuevoEstudiante(in iterations INT)
BEGIN
    DECLARE counter INT DEFAULT 0;
    DECLARE p_dni VARCHAR(100);
    DECLARE p_nombre_estudiante VARCHAR(100);
    DECLARE p_apellido_estudiante VARCHAR(100);
    WHILE counter < iterations DO
    SET p_DNI = FLOOR(RAND() * 99999999);
    SET p_nombre_estudiante = CONCAT('Nombre', ROUND(RAND() * 10000));
    SET p_apellido_estudiante = CONCAT('Apellido', ROUND(RAND() * 10000));

    INSERT INTO estudiantes (DNI, Nombre_Estudiante, Apellidos_Estudiante) VALUES (p_dni, p_nombre_estudiante, p_apellido_estudiante);
    SET counter = counter  + 1;
    END WHILE;
END//
DELIMITER ;

CALL InsertarNuevoEstudiante(5);

SELECT * FROM estudiantes;

+-----------+-------------------+----------------------+
| DNI       | Nombre_Estudiante | Apellidos_Estudiante |
+-----------+-------------------+----------------------+
| 11223344C | Carlos            | Martínez             |
| 12345678A | Juan              | García               |
| 25113375  | Nombre8943        | Apellido7179         |
| 45125857  | Nombre2282        | Apellido7871         |
| 75705809  | Nombre2472        | Apellido9650         |
| 8318682   | Nombre5210        | Apellido3555         |
| 87654321B | María             | López                |
| 90672084  | Nombre3799        | Apellido1794         |
+-----------+-------------------+----------------------+
```

3. Insertar nuevos emails en la tabla emails

```sql
DELIMITER //
CREATE PROCEDURE InsertarNuevoEmail(in iterations INT)
BEGIN
    DECLARE counter INT DEFAULT 0;
    DECLARE p_id INT;
    DECLARE p_email VARCHAR(100);
    WHILE counter < iterations DO
    SET p_id = FLOOR(RAND()* 100 - 50 + 1) + 50;
    SET p_email = CONCAT('email', (RAND() * 500), '@gmail.com');

    INSERT INTO email (ID, email) VALUES (p_id, p_email);
    SET counter = counter  + 1;
    END WHILE;
END//
DELIMITER ;

CALL InsertarNuevoEmail(5);

SELECT * FROM email;

+----+-----------------------------------+
| ID | email                             |
+----+-----------------------------------+
|  1 | ejemplo1@gmail.com                |
|  2 | ejemplo2@gmail.com                |
|  3 | ejemplo3@gmail.com                |
|  4 | email392.07619325451196@gmail.com |
| 54 | email62.83957097943832@gmail.com  |
| 57 | email422.43064373957986@gmail.com |
| 69 | email162.59364426377567@gmail.com |
| 83 | email383.89167132218523@gmail.com |
+----+-----------------------------------+
```

4. Insertar nuevas direcciones

```sql
DELIMITER //
CREATE PROCEDURE InsertarNuevaDireccion(in iterations INT)
BEGIN
    DECLARE counter INT DEFAULT 0;
    DECLARE p_id INT;
    DECLARE p_provincia VARCHAR(100);
    DECLARE p_numero INT;
    DECLARE p_cod_postal INT;
    DECLARE p_piso INT;
    DECLARE p_calle VARCHAR (100);
    DECLARE p_municipio VARCHAR (100);
    WHILE counter < iterations DO
    SET p_id = FLOOR(RAND()* 100 - 50 + 1) + 50;
    SET p_provincia = CONCAT('Provincia', (RAND() * 1000));
    SET p_numero = FLOOR(RAND() * 1000) + 1;
    SET p_cod_postal = FLOOR(RAND() * 99999);
    SET p_piso = FLOOR((RAND() * 100));
    SET p_calle = CONCAT('Calle', (RAND() * 10000));
    SET p_municipio = CONCAT('Municipio', (RAND() * 400));


    INSERT INTO direccion (ID, Provincia, Numero, Codigo_Postal, Piso, Calle, Municipio) VALUES (p_id, p_provincia, p_numero, p_cod_postal, p_piso, p_calle, p_municipio);
    SET counter = counter  + 1;
    END WHILE;
END//
DELIMITER ;

CALL InsertarNuevaDireccion(5);

+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
| ID | Provincia                   | Numero | Codigo_Postal | Piso | Calle                   | Municipio                   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
|  1 | Madrid                      |    123 |         28001 |    1 | Calle Viena             | Madrid                      |
|  2 | Barcelona                   |    456 |          8001 |    2 | Calle Segovia           | Barcelona                   |
|  3 | Valencia                    |    789 |         46001 |    3 | Calle Arcilleria        | Valencia                    |
| 28 | Provincia921.9593563321599  |    800 |         23287 |   76 | Calle1270.2226557491558 | Municipio135.88802491863075 |
| 32 | Provincia568.507571302827   |    890 |         74415 |    5 | Calle225.3997793657703  | Municipio383.87260994303284 |
| 72 | Provincia157.08241533216312 |    645 |         75127 |   82 | Calle8605.555918631662  | Municipio333.6571309097643  |
| 74 | Provincia774.8940622200204  |    683 |          8585 |   38 | Calle6571.746828567001  | Municipio54.8127722505599   |
| 98 | Provincia953.6042473778168  |    836 |         31913 |    8 | Calle4811.710989858686  | Municipio57.0822846676058   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
```

5. Insertar profesores en la tabla profesores (este caso esta dirigido para cuando se quiere añadir uno o varios profesor de forma manual, introduciendo los datos del profesor de forma directa)

```sql
DELIMITER //

CREATE PROCEDURE InsertarProfesor(
    IN p_apellidos VARCHAR(100),
    IN p_nombre VARCHAR(100),
    IN p_DNI VARCHAR(100),
    IN p_es_tutor ENUM('Si', 'No')
)
BEGIN
    INSERT INTO profesores (Apellidos, Nombre, DNI, Es_Tutor)
    VALUES (p_apellidos, p_nombre, p_dNI, p_es_Tutor);
END //

DELIMITER ;

CALL InsertarProfesor('Soria', 'Francisco', '07723315L', 'Si');

SELECT * FROM profesores;
+----+--------------+------------+-----------+----------+
| ID | Apellidos    | Nombre     | DNI       | Es_Tutor |
+----+--------------+------------+-----------+----------+
|  1 | García       | Juan       | 12345678A | Si       |
|  2 | López        | María      | 87654321B | No       |
|  3 | Martínez     | Carlos     | NULL      | Si       |
|  4 | Profesor1897 | Nombre2302 | 58183837  | Si       |
|  5 | Profesor3478 | Nombre830  | 37164252  | No       |
|  6 | Profesor9310 | Nombre8275 | 34448738  | Si       |
|  7 | Profesor1661 | Nombre1109 | 5613668   | No       |
|  8 | Profesor5714 | Nombre131  | 35141182  | No       |
|  9 | Profesor5342 | Nombre5180 | 98719377  | Si       |
| 10 | Profesor9488 | Nombre5979 | 14311839  | No       |
| 11 | Profesor1797 | Nombre1332 | 12692235  | Si       |
| 12 | Profesor7939 | Nombre2647 | 94178644  | No       |
| 13 | Profesor7488 | Nombre9997 | 75204978  | No       |
| 14 | Profesor5493 | Nombre4633 | 66838455  | No       |
| 15 | Profesor7555 | Nombre9213 | 33987918  | No       |
| 16 | Profesor6578 | Nombre4826 | 43942168  | No       |
| 17 | Profesor4287 | Nombre8955 | 19143164  | Si       |
| 18 | Profesor7785 | Nombre807  | 6790650   | Si       |
| 19 | Profesor2841 | Nombre1276 | 78597724  | No       |
| 20 | Soria        | Francisco  | 07723315L | Si       |
+----+--------------+------------+-----------+----------+
```
