1.  複数のJOINの活用（グルーピングなし）
・要件：
まず下準備に、filmテーブルから映画の一覧を取得し、好きな映画を一つ決めてください。
その映画の置いてあるinventory店舗storeと住所addressを、結合(JOIN)を使って取得してください。
グルーピングは不要です。(重複行は発生して構いません。)

　・提出物: この要件を満たすSQL文。

    SELECT *
    FROM film;


    SELECT c.store_id,d.address
    FROM inventory a
    INNER JOIN film b
    ON a.film_id=b.film_id
    INNER JOIN store c
    ON a.store_id=c.store_id
    INNER JOIN address d
    ON c.address_id=d.address_id
    WHERE b.title='Aladdin Calendar';


2. 複数テーブルのグルーピングと集計の適用
　・要件：payment テーブル、customer テーブル、rental テーブルを利用して、
顧客IDごとの合計支払い金額とその顧客の合計レンタル回数を計算し、
合計支払い金額を第1優先、
レンタル回数を第2優先として、
上位5人の顧客ID、その支払い合計、レンタル回数を取得してください。

　・提出物: この要件を満たすSQL文。


    SELECT a.customer_id,SUM(b.amount),COUNT(c.rental_id)
    FROM customer a
    JOIN payment b
    ON a.customer_id=b.customer_id
    JOIN rental c
    ON b.customer_id=c.customer_id
    GROUP BY a.customer_id
    ORDER BY a.customer_id LIMIT 5;