
/* ---------------- Sintaxis SQL INSERT INTO ----------------- */
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...);

/* -------------------- INSERTAR DATOS ----------------------- */
INSERT INTO Autor (nombre, biografia) 
VALUES ('Sun Tzu', 'Sun Tzu fue un general, estratega militar y filósofo de la antigua China.');

INSERT INTO Editorial (nombre)
VALUES ('Ediciones Libertador');

INSERT INTO Categoria (descripcion)
VALUES ('Militar'),('Filosofía');

INSERT INTO Libros (isbn, titulo, id_autor, id_editorial, precio, paginas, id_idioma, edicion)
VALUES ('978-987-1512-21-8', 'El arte de la guerra', 17, 8, 200, 159, 1, 2009);

INSERT INTO LibroCategoria (isbn, id_categoria)
VALUES ('978-987-1512-21-8', 6), ('978-987-1512-21-8', 7);


/* --------------------- Sintaxis SQL DELETE ------------------ */
DELETE FROM table_name WHERE condition;

/* ----------------------- ELIMINAR DATOS --------------------- */
DELETE FROM Editorial WHERE id = 7;

DELETE FROM Editorial WHERE id = 10 OR id = 11 OR id = 12 OR id = 13;

DELETE FROM Editorial WHERE id >= 10 AND id <= 13;

DELETE FROM Editorial WHERE id BETWEEN 10 AND 13;

DELETE FROM Editorial WHERE id IN (10,11,12,13);


/* -------------------- Sintaxis SQL UPDATE -------------------- */
UPDATE table_name SET column1 = value1, column2 = value2, ... WHERE condition;

/* ---------------------- MODIFICAR DATOS ---------------------- */
UPDATE Autor SET biografia = 'Su nombre de nacimiento era Sun Wu.' WHERE id = 17;

UPDATE Libros SET id_idioma = 3 WHERE id_idioma = 1;

UPDATE Autor SET biografia = 'Filósofo de la antigua China' WHERE id = 15;

UPDATE Libros SET id_idioma = 2 WHERE id_idioma = 3;	


/* ---------------------- Sintaxis SQL SELECT ------------------- */
SELECT column1, column2, ... FROM table_name;

/* ---------------------- SELECCIONAR DATOS --------------------- */
SELECT TOP 5 * FROM Autor; 

SELECT * FROM Editorial;

SELECT * FROM Categoria;

SELECT * FROM Libros; 

SELECT * FROM LibroCategoria;

SELECT count(*) FROM Libros;


/*  ---------- Usando la Base de Datos CursoSQL --------- */

USE CursoSQL;


/* ------------------- Consultas (DML) ------------------ */ 

SELECT * FROM Facturas;


SELECT * FROM Personas;


SELECT p.DNI, p.Nombre, f.NumFactura
FROM Personas AS p, Facturas AS f
WHERE p.DNI = f.DNI AND p.Nombre = 'María'
ORDER BY p.DNI;


SELECT p.DNI, p.Nombre, f.NumFactura
FROM Personas AS p JOIN Facturas AS f ON p.DNI = f.DNI
WHERE p.Nombre = 'María'
ORDER BY p.DNI;


SELECT * 
FROM Personas
WHERE DNI in (23800504, 23800506);


SELECT DNI, COUNT (*) AS cantidad 
FROM Facturas
GROUP BY DNI
HAVING COUNT (*) > 1;


SELECT COUNT (*) AS cantidad, 
       MIN (DNI) AS minimo, 
       MAX (DNI) AS maximo, 
       AVG (DNI) AS promedio, 
       SUM (DNI) AS suma
FROM Facturas;


SELECT * 
FROM Facturas AS f
WHERE f.DNI IN (SELECT p.DNI FROM Personas AS p);


SELECT p.DNI 
FROM Personas AS p
WHERE p.DNI IN (SELECT f.DNI FROM Facturas AS f)
ORDER BY p.DNI, p.Nombre;


SELECT p.DNI, p.Nombre 
FROM Personas AS p, facturas AS f
WHERE p.DNI = f.DNI
ORDER BY p.DNI;


SELECT p.DNI, p.Nombre, f.NumFactura
FROM Personas AS p FULL OUTER JOIN Facturas AS f ON p.DNI = f.DNI
WHERE p.DNI is NULL OR f.DNI is NULL
ORDER BY p.DNI;


SELECT p.DNI, p.Nombre, f.NumFactura
FROM Personas AS p LEFT JOIN Facturas AS f ON p.DNI = f.DNI
WHERE p.DNI is NULL OR f.DNI is NULL
ORDER BY p.DNI;


SELECT p.DNI, p.Nombre, f.NumFactura
FROM Personas AS p RIGHT JOIN Facturas AS f ON p.DNI = f.DNI
WHERE p.DNI is NULL OR f.DNI is NULL
ORDER BY p.DNI;
