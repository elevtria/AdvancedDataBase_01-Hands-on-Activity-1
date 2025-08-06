# AdvancedDataBase_01-Hands-on-Activity-1
Prelims Activity

//SQL While-loop and If-else
//Usage of CONCAT, (BETWEEN, AND)

//START
USE LabDB;
CREATE TABLE REC(
Id INT PRIMARY KEY,
LastName VARCHAR(100),
FirstName VARCHAR(100),
Age INT,
Gender VARCHAR(100),
Level VARCHAR(100)
)

INSERT INTO REC
VALUES
(1, 'Santos', 'Mark Anthony', 17, 'Male', 'Freshman'),
(2, 'Nonat', 'Jayson', 15, 'Male', 'Sophomore'),
(3, 'Valencia', 'Nicole', 20, 'Female', 'Senior'),
(4, 'Campos', 'Jane', 19, 'Female', 'Junior'),
(5, 'Morales', 'Micah', 21, 'Female', 'Senior'),
(6, 'Atienza', 'Eldibert', 17, 'Male', 'Sophomore'),
(7, 'Dela Cruz', 'Philip', 16, 'Male', 'Freshman'),
(8, 'Ramos', 'Loisa', 21, 'Female', 'Senior'),
(9, 'Galang', 'Orlean', 18, 'Male', 'Junior'),
(10, 'Detera', 'Chin', 16, 'Female', 'Freshman')

DECLARE @counter AS INT = 1
DECLARE @maxID INT = (SELECT MAX(Id) FROM REC)

DECLARE @id INT
DECLARE @FirstName VARCHAR(100)
DECLARE @LastName VARCHAR(100)
DECLARE @age INT
DECLARE @gender VARCHAR(100)
DECLARE @level VARCHAR(100)

WHILE @counter <= @maxID
	BEGIN
		SELECT 
        @id = Id,
        @FirstName = FirstName,
        @LastName = LastName,
        @age = Age,
        @gender = Gender
    FROM REC
    WHERE Id = @counter

    IF @age BETWEEN 14 AND 16
        SET @level = LOWER('Freshman')
    ELSE IF @age BETWEEN 17 AND 19
        SET @level = LOWER('Sophomore')
    ELSE IF @age BETWEEN 20 AND 22
        SET @level = LOWER('Junior')
    ELSE IF @age BETWEEN 23 AND 25
        SET @level = LOWER('Senior')
    ELSE
        SET @level = 'Unknown'

    PRINT CONCAT('ID: ', @id, ' | Name: ', @FirstName, ' ', @LastName, ' | Age: ', @age, ' | Gender: ', @gender, ' | Level: ', @level)

    SET @counter = @counter + 1
END
//END
