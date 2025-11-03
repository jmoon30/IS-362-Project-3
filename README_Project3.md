# IS 362 – Project 3 (Chinook)
John Moon <br>
Prof. Cohen <br>
IS 362 - Data Acquisition and Management <br>
Nov. 3, 2025

This repo/notebook demonstrates joining data across **five tables** in the Chinook database and loading the results into a pandas DataFrame.

## Files
- `IS362_Project3_Chinook.ipynb` — the runnable Jupyter notebook
- `chinook_project3_results.csv` — CSV export created by the notebook (after running)
- `Chinook_Sqlite.sqlite` — sample database (SQLite version)

## How to run (locally)
1. Install Python 3.10+ and Jupyter (e.g., `pip install notebook pandas`).
2. Ensure `Chinook_Sqlite.sqlite` is in the same folder as the notebook (or update `db_path` in the first code cell).
3. Launch Jupyter:  
   ```bash
   jupyter notebook
   ```
4. Open `IS362_Project3_Chinook.ipynb` and run all cells.
5. The output DataFrame shows **Customer LastName, FirstName, TrackName, AlbumTitle**, sorted by customer name. The notebook also saves `chinook_project3_results.csv`.

## SQL (for reference)

```sql
SELECT 
  c.LastName,
  c.FirstName,
  t.Name AS TrackName,
  a.Title AS AlbumTitle
FROM Customer AS c
JOIN Invoice AS i      ON i.CustomerId = c.CustomerId
JOIN InvoiceLine AS il ON il.InvoiceId = i.InvoiceId
JOIN Track AS t        ON t.TrackId = il.TrackId
JOIN Album AS a        ON a.AlbumId = t.AlbumId
ORDER BY c.LastName, c.FirstName, t.Name;
```

## Notes
- This satisfies the assignment by joining across **Customer → Invoice → InvoiceLine → Track → Album** and sorting by last and first name.
- If you use a different RDBMS (MySQL/PostgreSQL/SQL Server), adjust the **connection** code accordingly but the SQL is portable.
