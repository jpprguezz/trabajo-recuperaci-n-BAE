## Procedimientos

1. Insertar nuevos profesores en la trabla profesores

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

select * from profesores;
+----+--------------+------------+-----------+----------+
| ID | Apellidos    | Nombre     | DNI       | Es_Tutor |
+----+--------------+------------+-----------+----------+
|  1 | García       | Juan       | 12345678A | Si       |
|  2 | López        | María      | 87654321B | No       |
|  3 | Martínez     | Carlos     | NULL      | Si       |
|  4 | Profesor7100 | Nombre5216 | 47826775  | No       |
|  5 | Profesor6974 | Nombre75   | 94533739  | No       |
|  6 | Profesor6852 | Nombre3133 | 51104987  | No       |
|  7 | Profesor5430 | Nombre8694 | 71778725  | No       |
|  8 | Profesor7508 | Nombre8117 | 80599779  | No       |
|  9 | Profesor5563 | Nombre9971 | 31648724  | No       |
| 10 | Profesor62   | Nombre2576 | 26931259  | No       |
| 11 | Profesor612  | Nombre5845 | 73876252  | No       |
| 12 | Profesor4858 | Nombre6077 | 58123466  | Si       |
| 13 | Profesor6713 | Nombre1075 | 52373369  | Si       |
| 14 | Profesor9092 | Nombre6576 | 56066049  | No       |
| 15 | Profesor4700 | Nombre8588 | 88413129  | No       |
| 16 | Profesor5685 | Nombre3098 | 84354591  | Si       |
| 17 | Profesor9112 | Nombre6911 | 72162388  | No       |
| 18 | Profesor5097 | Nombre9438 | 18978304  | Si       |
| 19 | Profesor185  | Nombre7399 | 64405859  | Si       |
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
    SET p_nombre_estudiante = CONCAT('Apellido', ROUND(RAND() * 10000));
    SET p_apellido_estudiante = CONCAT('Nombre', ROUND(RAND() * 10000));

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
| 31340449  | Apellido9984      | Nombre519            |
| 64800453  | Apellido6210      | Nombre1609           |
| 77066652  | Apellido7670      | Nombre5229           |
| 82740442  | Apellido2355      | Nombre6955           |
| 87654321B | María             | López                |
| 94154405  | Apellido2250      | Nombre3005           |
+-----------+-------------------+----------------------+
```

2. Insertar nuevos emails en la tabla emails

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