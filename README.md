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

![image](https://github.com/user-attachments/assets/a4228b12-60f0-499f-bb6f-241fb29c7048)
