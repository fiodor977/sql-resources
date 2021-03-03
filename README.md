INDICE

----------------------------------------

1. CREATE TABLE
	1.1. Data types (varchar2, char, date, number, long, clob, raw, long, raw)
2. DROP TABLE
3. ALTER TABLE
	3.1. ADD
	3.2. DROP and DELETE
	3.3. MODIFY
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
	
	CREATE TABLE name (
		attrib datatype...
	);

	
	CREATE TABLE department (
		name VARCHAR2(20),
		numDepartmentInt NUMBER(3)
		numDepartmentFloat NUMBER(3,2)   // (3,2)   3: length of int, 2: length of float 
	);

	1.1. Data types





2. DROP TABLE

	DROP TABLE table;
	
	DROP TABLE department;


3. ALTER TABLE
	
	3.1. ADD

		ALTER TABLE table ADD attrib dataType;   // add a column to an existing table  
		ALTER TABLE Customers ADD Email varchar(255);
		
		ALTER TABLE table ADD (constraint);    // add a restriction to an existing column
		ALTER TABLE persons ADD (UNIQUE (ID));


		// alter table with CONSTRAINT statement
		ALTER TABLE article ADD(
  			CONSTRAINT articleFK FOREIGN KEY (CATEGORIE) REFERENCES CATEGORIE (CATEGORIE)
		);

		// alter table with various constraints in a single ALTER TABLE 
		ALTER TABLE thing ADD(
    			CONSTRAINT clientFK FOREIGN KEY (CLIENT) REFERENCES CLIENT(CLIENT_ID),
    			CONSTRAINT payFK FOREIGN KEY (pay) REFERENCES pay(PAY_ID)
		);


		ALTER TABLE talbe ADD CONSTRAINT restrictionName restriction(column/s);    // constraint with name
		ALTER TABLE department ADD CONSTRAINT UC_Person UNIQUE (ID,LastName);

	3.2. DROP and DELETE

		ALTER TABLE table DROP COLUMN column;
		ALTER TABLE department DROP COLUMN numDepartment;   // this deletes a column of a table

		

		DELETE FROM table WHERE column = 'content';
		DELETE FROM department WHERE name = 'Putin';  // this deletes the rows which name is Putin (all the row)



		DELETE FROM table;   //  this deletes all the data of a table but keeps the table
 
		
	3.3. MODIFY

		// modify the datatype of an element
		ALTER TABLE table MODIFY (column datatype);
		ALTER TABLE persons MODIFY (birthDate date);

		// add a default value to a column
		ALTER TABLE table MODIFY nombreColumna DEFAULT 'defaultValue';
		ALTER TABLE Persons MODIFY City DEFAULT 'Sadness';


4. CONSTRAINT
		
	4.1. NOT NULL



	4.2. UNIQUE



	4.3. PRIMARY KEY



	4.4. FOREIGN KEY



	4.5. CHECK



	4.6. DEFAULT



	4.7. INDEX



	4.8. AUTO INCREMENT
