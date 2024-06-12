1. Nombre completo de los profesores

```sql
DELIMITER //

CREATE FUNCTION ObtenerNombreCompletoProfesor(p_ID INT)
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    DECLARE v_nombre_completo VARCHAR(100);
    
    SELECT CONCAT(Nombre, ' ', Apellidos) INTO v_nombre_completo
    FROM profesores
    WHERE ID = p_ID;
    
    RETURN v_nombre_completo;
END //

DELIMITER ;

SELECT ObtenerNombreCompletoProfesor(1);

+----------------------------------+
| ObtenerNombreCompletoProfesor(1) |
+----------------------------------+
| Juan García                      |
+----------------------------------+
```

2. Total de estudiantes

```sql
DELIMITER //

CREATE FUNCTION ContarEstudiantes()
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE v_total_estudiantes INT;
    
    SELECT COUNT(*) INTO v_total_estudiantes
    FROM estudiantes;
    
    RETURN v_total_estudiantes;
END //

DELIMITER ;

SELECT ContarEstudiantes();
+---------------------+
| ContarEstudiantes() |
+---------------------+
|                   8 |
+---------------------+
```


3. Averiguar el dominio al que pertenece un email

```sql
DELIMITER //

CREATE FUNCTION ObtenerDominioEmail()
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    DECLARE v_dominio VARCHAR(100);
    
    -- Extraer el dominio del primer correo electrónico en la tabla
    SELECT SUBSTRING_INDEX(email, '@', -1) INTO v_dominio
    FROM email
    LIMIT 1;
    
    RETURN v_dominio;
END //

DELIMITER ;

SELECT ObtenerDominioEmail();

+-----------------------+
| ObtenerDominioEmail() |
+-----------------------+
| gmail.com             |
+-----------------------+
```


4. Provincia con más direcciones
```sql
DELIMITER //

CREATE FUNCTION ProvinciaConMasDirecciones()
RETURNS VARCHAR(100)
DETERMINISTIC
BEGIN
    DECLARE v_provincia VARCHAR(100);
    DECLARE v_contador INT;
    
    SELECT Provincia, COUNT(*) AS TotalDirecciones INTO v_provincia, v_contador FROM direccion
    GROUP BY Provincia ORDER BY TotalDirecciones DESC
    LIMIT 1;
    
    RETURN v_provincia;
END //

DELIMITER ;

SELECT ProvinciaConMasDirecciones();

+------------------------------+
| ProvinciaConMasDirecciones() |
+------------------------------+
| Madrid                       |
+------------------------------+
```


5. Profesores que son tutores

```sql
DELIMITER //

CREATE FUNCTION ContarProfesoresTutores()
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE v_count INT;
    
    SELECT COUNT(*) INTO v_count FROM profesores
    WHERE Es_Tutor = 'Si';
    
    RETURN v_count;
END //

DELIMITER ;

SELECT ContarProfesoresTutores();

+---------------------------+
| ContarProfesoresTutores() |
+---------------------------+
|                         9 |
+---------------------------+
```
