# LAB 5

1. Completați următorul cod pentru a afișa cel mai mare număr dintre cele trei numere prezentate:
```
DECLARE @N1 INT, @N2 INT, @N3 INT;
DECLARE @MAI_MARE INT;
SET @N1 = 60 * RAND()
SET @N2 = 60 * RAND()
SET @N3 = 60 * RAND()
if @N1 > @N2 set @MAI_MARE = @N1
else set @MAI_MARE = @N2
if @N2 > @N3 set @MAI_MARE = @N2
else set @MAI_MARE = @N3
if @N3 > @N1 set @MAI_MARE = @N3
else set @MAI_MARE = @N1
PRINT @N1;
PRINT @N2;
PRINT @N3;
PRINT 'Mai mare = ' + CAST(@MAI_MARE AS VARCHAR(2));
```
![Task1](https://user-images.githubusercontent.com/34598688/47987876-543bb100-e0e9-11e8-9a84-313f063c1ae3.png)

2. Afișati primele zece date (numele, prenumele studentului) în funcție de valoarea notei (cu exceptia notelor 6 și 8) a studentului la primul test al disciplinei Baze de date, folosind structura de altemativă IF...ELSE. Să se folosească variabilele.
```
select top 10 s.Nume_Student, s.Prenume_Student, sr.Nota
from studenti as s inner join studenti_reusita as sr
on s.Id_Student = sr.Id_Student
inner join discipline as d
on d.Id_Disciplina = sr.Id_Disciplina
where Tip_Evaluare = 'Testul 1' and d.Disciplina = 'Baze de date' and Nota <> 6 and Nota <> 8;
```
![Task2](https://user-images.githubusercontent.com/34598688/47902137-36244580-de8a-11e8-9812-54e5116b70a8.png)


3. Rezolvați aceeși sarcină, 1, apelând la structura selectivă CASE.
```
DECLARE @N1 INT, @N2 INT, @N3 INT;
DECLARE @MAI_MARE INT;
SET @N1 = 60 * RAND()
SET @N2 = 60 * RAND()
SET @N3 = 60 * RAND()
PRINT @N1;
PRINT @N2;
PRINT @N3;
PRINT 'Mai mare = ' + CAST(
case
when @N1 > @N2 and @N1 > @N3 then @N1
when @N2 > @N1 and @N2 > @N3 then @N2
when @N3 > @N2 and @N3 > @N1 then @N3
else NULL
end
AS VARCHAR(2));
```
![Task3](https://user-images.githubusercontent.com/34598688/47988059-dfb54200-e0e9-11e8-815c-be85209b3fba.png)

4. Modificați exercițiile din sarcinile 1 și 2 pentru a include procesarea erorilor cu TRY și CATCH și RAISERRROR.
```
begin try
DECLARE @N1 INT, @N2 INT, @N3 INT;
DECLARE @MAI_MARE INT;
SET @N1 = 60 * RAND()
SET @N2 = 60 * RAND()
SET @N3 = 60 * RAND()
if @N1 > @N2 and @N1 > @N3 set @MAI_MARE = @N1
else if @N2 > @N1 and @N2 > @N3 set @MAI_MARE = @N2
else if @N3 > @N1 and @N3 > @N2 set @MAI_MARE = @N3
else
raiserror('Asa valoare a fost declarata de 2 ori', 16, 1);
end try
begin catch
print ' ERROR :' + cast(ERROR_LINE() as varchar(20));
end catch
PRINT @N1;
PRINT @N2;
PRINT @N3;
PRINT 'Mai mare = ' + CAST(@MAI_MARE AS VARCHAR(2));
```
![Task1_try_catch_raiserror](https://user-images.githubusercontent.com/34598688/47993843-49891800-e0f9-11e8-9e06-f5d94de49368.png)

```
begin try
select top 10 s.Nume_Student, s.Prenume_Student, sr.Nota
from studenti as s inner join studenti_reusita as sr
on s.Id_Student = sr.Id_Student
inner join discipline as d
on d.Id_Disciplina = sr.Id_Disciplina
where Tip_Evaluare = 'Testul 1' and d.Disciplina = 'Baze de date' and Nota <> 6 and Nota <> 8;
raiserror ('Asa student nu exista', 16, 1);
end try
begin catch
print 'Error'
end catch
```
![Task2_try_catch_raiserror](https://user-images.githubusercontent.com/34598688/47994018-d9c75d00-e0f9-11e8-8613-78a5746194cd.png)
