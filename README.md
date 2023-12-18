# sql-tasks

## Kilka zadań związanych z SQLem 🧑‍💻:

### 1. Wyświetl tytuły i ceny wypożyczenia filmów, których cena wypożyczenia przekracza 9 zł. Wynik uporządkuj rosnąco według ceny wypożyczenia.

```sql
SELECT tytul, cena
FROM filmy
WHERE cena > 9
ORDER BY cena ASC
```
