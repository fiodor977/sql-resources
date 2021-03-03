INDICE

----------------------------------------

1. CREATE TABLE
	1.1. Tipos de datos (varchar2, char, date, number como mínimo, el resto: long, clob, raw, long raw)
2. DROP TABLE
3. ALTER TABLE
	3.1. Añadir elementos
	3.2. Eliminar elementos
	3.3. Modificar elementos
4. CONSTRAINT
	4.1. NOT NULL
	4.2. UNIQUE
	4.3. PRIMARY KEY
	4.4. FOREIGN KEY
	4.5. CHECK
	4.6. DEFAULT
	4.7. INDEX
	4.8. AUTO INCREMENT

-----------------------------------------




1. CREATE TABLE
	
	CREATE TABLE nombre (
		atributo tipo...
	);

	
	CREATE TABLE departamento (
		nombre VARCHAR2(20),
		numDepartamento NUMBER(3)
		numDepartamentoDecimal NUMBER(3,2)
	);

	1.1. Tipos de datos





2. DROP TABLE

	DROP TABLE nombreTabla;
	
	DROP TABLE departamento;


3. ALTER TABLE
	
	3.1. Añadir elementos

		ALTER TABLE nombreTabla ADD atributo tipoAtributo;   // añade una columna a una tabla ya existente
		
		
		ALTER TABLE nombreTabla ADD (restriccion);    // añade una restriccion a una columna ya existente
		ALTER TABLE Persons ADD (UNIQUE (ID));     // restriccion sin nombre


		// alter table con un constraint
		ALTER TABLE ARTICULO ADD(
  			CONSTRAINT FK_ARTICULO_CATEGORIA FOREIGN KEY (CATEGORIA) REFERENCES CATEGORIA (CATEGORIA)
		);

		// alter table con varios constraint en una sola frase (separados por comas)
		ALTER TABLE ALBARAN ADD(
    			CONSTRAINT FK_ALBARAN_CLIENTE FOREIGN KEY (CLIENTE) REFERENCES CLIENTE(NIF),
    			CONSTRAINT FK_ALBARAN_FORMA_PAGO FOREIGN KEY (FORMA_PAGO) REFERENCES FORMA_PAGO(FORMA_PAGO)
		);


		ALTER TABLE nombreTabla ADD CONSTRAINT nombreRestriccion restriccion(columna/s);    // restriccion con nombre
		ALTER TABLE departamento ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);

	3.2. Eliminar elementos

		ALTER TABLE nombreTabla DROP COLUMN nombreColumna;
		
		ALTER TABLE departamento DROP COLUMN numDepartamentoDecimal;   // esto borra una columna de una tabla concreta

		

		DELETE FROM nombreTabla WHERE nombreColumna = 'contenido';

		DELETE FROM departamento WHERE nombre = 'pepito';  // esto borra las filas enteras de la base de datos cuyo nombre sea pepito 



		DELETE FROM nombreTabla;   //  esto borra todo el contenido de una tabla, pero mantiene la tabla
 
		
	3.3. Modificar elementos

		// modificar un tipo de dato de una columna
		ALTER TABLE nombreTabla MODIFY (nombreColumna tipoDato);
		ALTER TABLE persons MODIFY (fechaNacimiento date);

		// poner valor por defecto a una columna
		ALTER TABLE nombreTabla MODIFY nombreColumna DEFAULT 'datoPorDefecto';
		ALTER TABLE Persons MODIFY City DEFAULT 'Sandnes';


	4. CONSTRAINT
		
		4.1. NOT NULL



		4.2. UNIQUE



		4.3. PRIMARY KEY



		4.4. FOREIGN KEY



		4.5. CHECK



		4.6. DEFAULT



		4.7. INDEX



		4.8. AUTO INCREMENT
