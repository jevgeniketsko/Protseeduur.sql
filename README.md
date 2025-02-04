Create database ProtseduurKetsko

Use ProtseduurKetsko
Create Table linn( 
LinnId int primary Key identity(1,1),
LinnNimi varchar(30),
rahvaArv int);
Select * from linn;
Insert into linn(linnNimi,rahvaArv)
Values('Tallinn',60652)
--Protseduuri loomine
--Protseedur, mis lisab uus liin ja kohe näitab tabelis

Create procedure lisaLinn
@lnimi varchar(30),
@rArv int

AS
BEGIN 

Insert into linn (linnNimi, rahvaArv)
Values (@lNimi, @rArv);
Select * From linn;



End;

--protseduuri kutse 
Exec lisaLinn @lnimi='Tartu', @rArv=1256
--lihtsam 
EXEC lisaLinn 'Tartu2', 1256
--kirje kustutamine
Delete from linn where linnID=3;
select * from linn;

--protseduur, mis kustutab liin id järgi
Create Procedure KustutaLinn
@taht char(1)
as
begin 

Select * from linn 
Where linnNimi like @taht +'%';
--% Kõik teised tähed 
END; 
--kutse 
EXEC linnaOtsing T;

![image](https://github.com/user-attachments/assets/65eae3b1-534b-4d24-9f4a-7cb551e09288)

![image](https://github.com/user-attachments/assets/443e86c8-ecdc-4429-80ec-9f866db8e79b)

![image](https://github.com/user-attachments/assets/bb66fee6-9856-4c70-8567-a3e953871f99)

