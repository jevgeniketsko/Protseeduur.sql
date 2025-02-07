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

--tabeli uuendamine - rahvaarv kasvab 10% võrra
UPDATE linn SET rahvaArv=rahvaArv*1.1
SELECT * From linn;
UPDATE linn SET rahvaArv=rahvaArv*1.1
Where linnID=7;

CREATE PROCEDURE rahvaArvuUuendus
@linnID int,
@koef decimal(2,1)
AS
BEGIN
UPDATE linn SET rahvaArv=rahvaArv*@koef
Where linnID=@linnID;
SELECT * From linn;
END;

drop procedure rahvaArvuUuendus;

EXEC rahvaArvuUuendus 7, 1.2;


![image](https://github.com/user-attachments/assets/65eae3b1-534b-4d24-9f4a-7cb551e09288)

![image](https://github.com/user-attachments/assets/443e86c8-ecdc-4429-80ec-9f866db8e79b)

![image](https://github.com/user-attachments/assets/bb66fee6-9856-4c70-8567-a3e953871f99)

Use Protseduur
Create Table linn( 
LinnId int primary Key identity(1,1),
LinnNimi varchar(30),

-- uue veeru lisamine
Alter table linn ADD test int;
--veeru kustutamine
alter table linn drop column test;

Create procedure veeruLisaKustutaTabelis
@valik varchar(20),
@tabelinimi varchar(20),
@veerunimi varchar(20),
@tyyp varchar(20),

AS
BEGIN
Insert into linn (linnNimi, rahvaArv) Values (@lNimi, @rArv); Select * From linn;
Declare @sqltegevus as varchar(max)
set @sqltegevus=case 
when @valik='add' then concat('alter table linn ADD ', @veerunimi, '', @tyyp);
when @valik'drop' then concat('alter table linn drop column ', @veerunimi);
END;
print @sqltegevus;
begin
exec (@sqltegevus);
END
END;


--kutse		
EXEC veeruLisakustuta @valik='add', @veerunimi= 'test3', @typp='int';
Select * from linn;
Exec veeruLisaKustutaTabelis @valik= 'drop', @tabelinimi='linn', @veerunimi='test3';
Select *from linn;

--protseduur tingimusega 
Create procedure rahvaHinnang 


AS
BEGIN
Select linnNimi, rahvaArv, IIF(rahvaArv<2000, 'väike linn', 'suur linn') as Hinnang 
From linn;


END;

Drop prodecure rahvaHinnang;

Exec rahvaHinnang 2000;
--Agregaat funkstioonid: SUM(), AVG(), MIN(), MAX(), COUNT()

Create procedure kokkuRahvaarv

AS 
BEGIN
Select SUM(rahvaArv) AS 'kokku rahvaArv', AVG(RahvaArv) AS 'keskmine rahvaArvä', Count(*)
From linn;
END;

Exec kokkuRahvaarv;

