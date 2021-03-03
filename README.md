#SQL CheatSheet

1. CREATE TABLE
	1.1. Data types
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

		varchar2
			strings...
		number
			integers and floats...
		date		
		
		char
		int
		long
		clob
		raw
		
	

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


		ALTER TABLE table ADD CONSTRAINT restrictionName restriction(column/s);    // constraint with name
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


4. CONSTRAINT

	//inline
	CREATE TABLE person (
		nif varchar2(9) PRIMARY KEY
	);
	
	
	//out of line
	CREATE TABLE employee (
		emp_id NUMBER(10),
		first_name VARCHAR2(200),
		last_name VARCHAR2(200),
		dept_id NUMBER(10),
		CONSTRAINT pk_emp PRIMARY KEY (emp_id)
	);
	

	4.1. NOT NULL
		//inline
		CREATE TABLE Persons (
    			ID int NOT NULL,
    			LastName varchar(255) NOT NULL,
    			FirstName varchar(255) NOT NULL,
    			Age int	
		);
		
		//out of line
		CREATE TABLE Persons (
    			ID int,
    			LastName varchar(255),
    			FirstName varchar(255),
    			Age int	
			
			CONSTRAINT ageNotNull CHECK (Age IS NOT NULL)
		);
		
		// modified after creation
		ALTER TABLE Persons MODIFY Age int NOT NULL;


	4.2. UNIQUE
		
		//inline
		CREATE TABLE Persons (
  			ID int UNIQUE,
    			LastName varchar(255) UNIQUE,
    			FirstName varchar(255),
    			Age int
		);
		
		//outline
		CREATE TABLE Persons (
    			ID int NOT NULL,
    			LastName varchar(255),
    			FirstName varchar(255),
    			Age int,	
			CONSTRAINT UQ_Person UNIQUE (ID,LastName)
		);
		
		//modified after creation 
		ALTER TABLE person ADD CONSTRAINT Person_UQ UNIQUE(ID, LastName);

	4.3. PRIMARY KEY

		//inline
		CREATE TABLE Persons (
    			ID int NOT NULL PRIMARY KEY,
    			LastName varchar(255),
    			FirstName varchar(255),
    			Age int
		);

		//outline
		
		CREATE TABLE Persons (
    			ID int NOT NULL,
    			LastName varchar(255),
    			FirstName varchar(255),
    			Age int,
			
			CONSTRAINT ID_PK PRIMARY KEY (ID)
		);		
		
		//modified after creation
		ALTER TABLE Persons ADD PRIMARY KEY (ID);   //without name
		
		ALTER TABLE Persons ADD CONSTRAINT PK_Person PRIMARY KEY (ID);   //with name

	4.4. FOREIGN KEY

		//in line
		CREATE TABLE Orders (
    			OrderID int NOT NULL PRIMARY KEY,
    			OrderNumber int NOT NULL,
    			PersonID int FOREIGN KEY REFERENCES Persons(PersonID)
		);
		
		//outline
		CREATE TABLE Orders (
    			OrderID int PRIMARY KEY,
    			OrderNumber int,
    			PersonID int,
    			CONSTRAINT FK_PersonOrder FOREIGN KEY (PersonID) REFERENCES Persons(PersonID)
		);
		
		//modified after creation
		ALTER TABLE Orders ADD FOREIGN KEY (PersonID) REFERENCES Persons(PersonID);

	4.5. CHECK

		//inline
		CREATE TABLE Persons (
    			ID int NOT NULL,
    			LastName varchar(255) NOT NULL,
    			FirstName varchar(255),
    			Age int CHECK (Age>=18)
		);
		
		//outline
		CREATE TABLE Persons (
    			ID int NOT NULL,
    			LastName varchar(255) NOT NULL,
    			FirstName varchar(255),
    			Age int,
    			City varchar(255),
    			CONSTRAINT CHK_Person CHECK (Age>=18 AND City='Sandnes')
			);
			
		// modified after creation
		ALTER TABLE Persons ADD CHECK (Age>=18);   //without name
		
		ALTER TABLE Persons ADD CONSTRAINT CHK_PersonAge CHECK (Age>=18 AND City='Sandnes');   //with name
	
	4.6. DEFAULT

		//inline
		CREATE TABLE Persons (
    			ID int,
    			LastName varchar(255),
    			FirstName varchar(255),
    			Age int,
    			City varchar(255) DEFAULT 'Sandnes'
		);
		
		
		//modified after creation
		ALTER TABLE Persons MODIFY City DEFAULT 'Sadness';   //sadness is the default value of city

	4.7. INDEX
	
		CREATE INDEX IndexName ON table(column);
		CREATE INDEX nameClientIndex ON CLIENTE(Nombre);
		
		CREATE INDEX idx_pname ON Persons (LastName, FirstName);  //index various elements
		
		//DROP index
		DROP INDEX index_name;

	4.8. AUTO INCREMENT

		CREATE SEQUENCE id_name
		MINVALUE 1
		START WITH 1
		INCREMENT BY 1
		CACHE 10;
		
