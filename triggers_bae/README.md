1. Actualizar el dominio de los emails de gmail a hotmail

```sql
DELIMITER //

CREATE TRIGGER cambiar_dominio_email_hotmail
BEFORE INSERT ON email
FOR EACH ROW
BEGIN
    DECLARE v_new_email VARCHAR(100);
    SET v_new_email = NEW.email;
    IF NEW.email LIKE '%gmail.com' THEN
        SET v_new_email = REPLACE(NEW.email, 'gmail.com', 'hotmail.com');
    END IF;
    SET NEW.email = v_new_email;
END //
DELIMITER ;

-- Si tratamos de insertar algun correo con el dominio "gmail", el trigger cambia automaticamente el dominio a hotmail

INSERT INTO email (email) VALUES ('ejemplo1@gmail.com');

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
| 86 | ejemplo1@hotmail.com              |
+----+-----------------------------------+
```

2. Convertir apellido a mayuscula en los estudiantes

```sql
DELIMITER //

CREATE TRIGGER mayusculas_estudiantes
BEFORE UPDATE ON estudiantes
FOR EACH ROW
BEGIN
    SET NEW.Apellidos_Estudiante = UPPER(NEW.Apellidos_Estudiante);
END //

DELIMITER ;

-- Al realizar el update, el apellido cambia automaticamente a mayusculas

SELECT * FROM estudiantes;
+-----------+-------------------+----------------------+
| DNI       | Nombre_Estudiante | Apellidos_Estudiante |
+-----------+-------------------+----------------------+
| 11223344C | Carlos            | Martínez             |
| 12345678A | Juan              | GARCÍA               |
| 25113375  | Nombre8943        | Apellido7179         |
| 45125857  | Nombre2282        | Apellido7871         |
| 75705809  | Nombre2472        | Apellido9650         |
| 82231149A | Alonso            | manzano              |
| 8318682   | Nombre5210        | Apellido3555         |
| 87654321B | María             | López                |
| 90672084  | Nombre3799        | Apellido1794         |
+-----------+-------------------+----------------------+
```


3. Convertir apellido a mayuscula en profesores

```sql
DELIMITER //

CREATE TRIGGER mayusculas_profesores
BEFORE UPDATE ON profesores
FOR EACH ROW
BEGIN
    SET NEW.Apellidos = UPPER(NEW.Apellidos);
END //

DELIMITER ;

UPDATE profesores SET Apellidos = 'Soria' WHERE ID = 20;

SELECT * FROM profesores;
+----+--------------+------------+-----------+----------+
| ID | Apellidos    | Nombre     | DNI       | Es_Tutor |
+----+--------------+------------+-----------+----------+
|  1 | García       | Juan       | 12345678A | No       |
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
| 20 | SORIA        | Francisco  | 07723315L | Si       |
+----+--------------+------------+-----------+----------+
```

4. Convertir nombre de las provincias a minuscula en las direcciones

```sql
DELIMITER //

CREATE TRIGGER minusculas_direccion
BEFORE UPDATE ON direccion
FOR EACH ROW
BEGIN
    SET NEW.Calle = LOWER(NEW.Calle);
END //

DELIMITER ;

UPDATE direccion SET Calle = 'Calle Arcilleria ' WHERE ID = 3;

SELECT * FROM direccion;

+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
| ID | Provincia                   | Numero | Codigo_Postal | Piso | Calle                   | Municipio                   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
|  1 | Madrid                      |    123 |         28001 |    1 | Calle Viena             | Madrid                      |
|  2 | Barcelona                   |    456 |          8001 |    2 | Calle Segovia           | Barcelona                   |
|  3 | Valencia                    |    789 |         46001 |    3 | calle arcilleria        | Valencia                    |
| 28 | Provincia921.9593563321599  |    800 |         23287 |   76 | Calle1270.2226557491558 | Municipio135.88802491863075 |
| 32 | Provincia568.507571302827   |    890 |         74415 |    5 | Calle225.3997793657703  | Municipio383.87260994303284 |
| 72 | Provincia157.08241533216312 |    645 |         75127 |   82 | Calle8605.555918631662  | Municipio333.6571309097643  |
| 74 | Provincia774.8940622200204  |    683 |          8585 |   38 | Calle6571.746828567001  | Municipio54.8127722505599   |
| 98 | Provincia953.6042473778168  |    836 |         31913 |    8 | Calle4811.710989858686  | Municipio57.0822846676058   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
```

5. Si la provincia es Barcelon, cambiamos a Tarragona

```sql
DELIMITER //

CREATE TRIGGER cambiar_provincia
BEFORE INSERT ON direccion
FOR EACH ROW
BEGIN
    DECLARE v_nueva_provincia VARCHAR(100);
    SET v_nueva_provincia = NEW.Provincia;
    IF NEW.Provincia = 'Barcelona' THEN
        SET v_nueva_provincia = 'Tarragona';
    END IF;
    SET NEW.Provincia = v_nueva_provincia;
END //

DELIMITER ;

-- Como vimos en el trigger de email, aqui pasa lo mismo. A partir de ahora cuando alguien intente introducir Barcelona, en la BBDD aparecera Tarragona

INSERT INTO direccion (ID, Provincia, Numero, Codigo_Postal, Piso, Calle, Municipio)
VALUES (50, 'Barcelona', 123, 28001, 50, 'Calle Ejemplo', 'Ejemplo');

SELECT * FROM direccion;

+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
| ID | Provincia                   | Numero | Codigo_Postal | Piso | Calle                   | Municipio                   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
|  1 | Madrid                      |    123 |         28001 |    1 | Calle Viena             | Madrid                      |
|  2 | Barcelona                   |    456 |          8001 |    2 | Calle Segovia           | Barcelona                   |
|  3 | Valencia                    |    789 |         46001 |    3 | calle arcilleria        | Valencia                    |
| 28 | Provincia921.9593563321599  |    800 |         23287 |   76 | Calle1270.2226557491558 | Municipio135.88802491863075 |
| 32 | Provincia568.507571302827   |    890 |         74415 |    5 | Calle225.3997793657703  | Municipio383.87260994303284 |
| 50 | Tarragona                   |    123 |         28001 |   50 | Calle Ejemplo           | Ejemplo                     |
| 72 | Provincia157.08241533216312 |    645 |         75127 |   82 | Calle8605.555918631662  | Municipio333.6571309097643  |
| 74 | Provincia774.8940622200204  |    683 |          8585 |   38 | Calle6571.746828567001  | Municipio54.8127722505599   |
| 98 | Provincia953.6042473778168  |    836 |         31913 |    8 | Calle4811.710989858686  | Municipio57.0822846676058   |
+----+-----------------------------+--------+---------------+------+-------------------------+-----------------------------+
```




