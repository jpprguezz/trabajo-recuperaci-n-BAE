1. Mensaje de confirmacion de insercion de profesores

```sql
DELIMITER //

CREATE TRIGGER profesor_tutor
AFTER INSERT ON profesores
FOR EACH ROW
BEGIN
    IF NEW.Es_Tutor = 'Si' THEN
        UPDATE profesores SET Es_Tutor = 'No' WHERE ID <> NEW.ID;
    ELSE
        UPDATE profesores SET Es_Tutor = 'Si' WHERE ID = NEW.ID;
    END IF;
END;
//

DELIMITER ;

-- Antes
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

-- Después 

UPDATE profesores SET Es_Tutor = 'No' WHERE ID = 1;

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
| 20 | Soria        | Francisco  | 07723315L | Si       |
+----+--------------+------------+-----------+----------+
``` 
2. Muestra un mensaje despues de insertar un estudiante
```sql
DELIMITER //

CREATE TRIGGER estudiantes_despues_de_insertar
AFTER INSERT ON estudiantes
FOR EACH ROW
BEGIN
    DECLARE mensaje VARCHAR(200);
    SET mensaje = CONCAT('Se ha insertado un nuevo estudiante con DNI ', NEW.DNI);
END //
DELIMITER ;


```




