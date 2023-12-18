# sql-tasks

## Kilka zadań związanych z SQLem 🧑‍💻:

### <a name="kropka1"><p align="justify">1. Wyświetl tytuły i ceny wypożyczenia filmów, których cena wypożyczenia przekracza 9 zł. Wynik uporządkuj rosnąco według ceny wypożyczenia.<p align="justify"></p></a>

```sql
SELECT tytul, cena
FROM filmy
WHERE cena > 9
ORDER BY cena ASC
```
