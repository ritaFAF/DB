##### Query-uri pentru lab 4


# 1: nr de ordine

--8. Obtineti identificatorii si numele studentilor, ale examenelor sustinute in anul 2018
select s.Id_Student, s.Nume_Student, sr.Data_Evaluare
from studenti as s inner join studenti_reusita as sr
on s.Id_Student=sr.Id_Student
where Data_Evaluare like '2018-%-%';

![Query#1]https://user-images.githubusercontent.com/34598688/46934389-40f47300-d060-11e8-83fd-b7d8917eec3d.png)

# 2 nr de ordine + 16

# 3 random de la 28 la 39