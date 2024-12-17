VERİTABANI VE TABLO OLUŞTURMA 

```
CREATE TABLE Sales (
sale_id INT PRIMARY KEY,
book_id INT,
sale_date DATE,
quantity INT
FOREIGN KEY (book_id) REFERENCES Books(book_id)
)

CREATE TABLE Books (
    book_id INT PRIMARY KEY,
    title VARCHAR(100),
    author VARCHAR(100),
    genre VARCHAR(50),
    price DECIMAL(5, 2)
)

INSERT INTO Books (book_id, title, author, genre, price) VALUES
(1, 'Book A', 'Author X', 'Fiction', 10.99),
(2, 'Book B', 'Author Y', 'Non-Fiction', 12.99),
(3, 'Book C', 'Author Z', 'Fiction', 8.99)

INSERT INTO Sales (sale_id, book_id, sale_date, quantity) VALUES
(1, 1, '2023-05-01', 2),
(2, 2, '2023-05-02', 1),
(3, 3, '2023-05-03', 4)
```




TEMEL SQL SORGULARI


```
SELECT * FROM Books WHERE author = 'Author X'

SELECT * FROM Sales WHERE sale_date ='20230501' 
```


FİYATI EN YÜKSEK 2 KİTAP 

```
SELECT TOP 2 * FROM Books ORDER BY price DESC
```


TÜRLERE GÖRE TOPLAM KİTAP SAYISI 

```
SELECT genre, COUNT(*) AS total_books FROM Books GROUP BY genre
```

TABLOLARI BİRLEŞTİRME

```
SELECT Books.title, Sales.sale_date, Sales.quantity FROM Sales JOIN Books ON Sales.book_id=Books.book_id
```


"2023-05-01" TARİHİNDEN SONRA EN ÇOK SATAN KİTAP


```
SELECT title FROM Books WHERE book_id = (SELECT TOP 1 book_id FROM Sales WHERE sale_date > '20230501' ORDER BY quantity DESC)
```


TÜRLERE GÖRE BÜYÜKTEN KÜÇÜĞE KİTAP SATIŞ MİKTARI 

``` 
SELECT genre, SUM(quantity) AS total_sold FROM Sales JOIN Books ON Sales.book_id = Books.book_id GROUP BY genre ORDER BY total_sold DESC
```



