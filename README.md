# sql-tasks

## Kilka zadań związanych z SQL 🧑‍💻:

### 1. Wyświetl tytuły i ceny wypożyczenia filmów, których cena wypożyczenia przekracza 9 zł. Wynik uporządkuj rosnąco według ceny wypożyczenia.

```sql
SELECT tytul, cena
FROM filmy
WHERE cena > 9
ORDER BY cena ASC
```
### 2. Wyświetl imiona i nazwiska wszystkich klientów, których imię liczy więcej znaków niż nazwisko.

```sql
SELECT imie, nazwisko
FROM klienci
WHERE LENGTH(imie) > LENGTH(nazwisko)
```
### 3. Wyświetl identyfikatory wszystkich kopii, które zostały wypożyczone pomiędzy ‘2005-07-15’ a ‘2005-07-22’. Wyeliminuj duplikaty. Wynik uporządkuj rosnąco w kolejności identyfikatorów kopii.

```sql
SELECT DISTINCT id_kopii
FROM wypozyczenia
WHERE data_wypozyczenia
BETWEEN '2005-07-15' AND '2005-07-22'
ORDER BY id_kopii ASC
```
### 4. Wyświetl te imiona klientów, których pierwsza i ostatnia litera imienia są identyczne. Ignoruj wielkość porównywanych znaków. Wyeliminuj duplikaty.

```sql
SELECT imie
FROM klienci
WHERE UPPER(SUBSTRING(imie, 1, 1)) = UPPER(SUBSTRING(imie, LENGTH(imie), 1))
```
### 5. Wyświetl tytuły i lata produkcji wszystkich filmów wypożyczonych przez klienta o nazwisku ‘Kowalski’.

```sql
SELECT tytul, rok_produkcji
FROM wypozyczenia JOIN klienci ON wypozyczenia.id_klienta = klienci.id_klienta
JOIN kopie ON wypozyczenia.id_kopii = kopie.id_kopii
JOIN filmy ON kopie.id_filmu = filmy.id_filmu
WHERE nazwisko = 'Kowalski'
```
### 6. Wyświetl tytuły filmów, w których razem zagrali aktorzy o nazwiskach ‘De Niro’ i ‘Reno’.

```sql
SELECT tytul
FROM filmy NATURAL JOIN obsada NATURAL JOIN aktorzy
WHERE nazwisko = 'Reno'
INTERSECT
SELECT tytul
FROM filmy NATURAL JOIN obsada NATURAL JOIN aktorzy
WHERE nazwisko = 'De Niro'
```
### 7. Wyświetl tytuły tych filmów, które były wypożyczane zarówno przez klienta o nazwisku ‘Kowalski’, jak i przez klienta o nazwisku ‘Nowak’.

```sql
SELECT tytul
FROM wypozyczenia NATURAL JOIN kopie NATURAL JOIN filmy NATURAL JOIN klienci
WHERE nazwisko = 'Kowalski'
INTERSECT
SELECT tytul
FROM wypozyczenia NATURAL JOIN kopie NATURAL JOIN filmy NATURAL JOIN klienci
WHERE nazwisko = 'Nowak'
```
### 8. Dla każdego roku produkcji filmu wyświetl średnią cenę wypożyczenia.

```sql
SELECT rok_produkcji, avg(cena)
FROM filmy
GROUP BY rok_produkcji
ORDER BY avg DESC

```
### 9. Ile razy wypożyczono film pt. ‘Taksowkarz'?

```sql
SELECT COUNT (wypozyczenia.id_kopii)
FROM wypozyczenia
NATURAL JOIN kopie
NATURAL JOIN filmy
WHERE filmy.tytul = 'Taksowkarz'
```
### 10. Wyświetl nazwisko klienta, który dokonał pierwszego wypożyczenia w historii wypożyczalni. Nie korzystaj z operatora LIMIT.

```sql
SELECT nazwisko
FROM wypozyczenia
NATURAL JOIN klienci
WHERE data_wypozyczenia = (SELECT MIN (data_wypozyczenia) FROM wypozyczenia)
```
### 11. Wyświetl tytuły filmów, których wypożyczenie kosztuje więcej niż wypożyczenie filmu o tytule ‘Frantic’.

```sql
SELECT tytul
FROM filmy
WHERE cena > ANY (SELECT cena FROM filmy WHERE tytul = 'Frantic');
```
### 12. Wyświetl tytuły filmów, których wypożyczenie kosztuje więcej niż wypożyczenie każdego filmu o tytule liczącym 6 liter.

```sql
SELECT tytul
FROM filmy
WHERE cena > ALL (SELECT cena FROM filmy WHERE LENGTH(tytul) = 6)
```
### 13. Do relacji FILMY wstaw nową krotkę: id_filmu=11, tytul=’Komornik’, rok_produkcji=2005, cena=10.5.

```sql
INSERT INTO filmy ( id_filmu, tytul, rok_produkeji, cena)
VALUES (11, 'Komornik', 2005, 10.5)
```
### 14. Z relacji FILMY usuń krotki opisujące filmy nakręcone w roku 2005.

```sql
DELETE FROM filmy
WHERE rok_produkeji = '2005'
```
### 15. Podnieś o 0,5 zł cenę wypożyczenia wszystkich filmów nakręconych przed rokiem 1980.

```sql
UPDATE filmy
SET cena = cena + 0.5
WHERE rok_produkeji < 1980
```
### 16. Zmień cenę wypożyczenia filmu pt. ‘Taksowkarz’ na 5 zł.

```sql
UPDATE filmy
SET cena = 5
WHERE tytul = 'Taksowkarz'
```
