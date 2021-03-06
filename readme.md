# Explorer Mode
1. How many users are there? **50**
```sql
SELECT count(*) FROM users;
```
2. What are the 5 most expensive items? **Small Cotton Gloves, Small Wooden Computer, Awesome Granite Pants, Sleek Wooden Hat, Ergonomic Steel Car**
```sql
SELECT title FROM items ORDER BY price DESC LIMIT 5;
```
3. What's the cheapest book? (Does that change for "category is exactly 'book'" versus "category contains 'book'"?) **Ergonomic Granite Chair; and, no, it doesn't change**
```sql
SELECT title FROM items WHERE category LIKE "%Book%" ORDER BY price ASC LIMIT 1;
```
4. Who lives at "6439 Zetta Hills, Willmouth, WY"? Do they have another address? **Corrine Little; and, yes: 54369 Wolff Forges, Lake Bryon, CA 31587.**
```sql
SELECT last_name, first_name FROM addresses INNER JOIN users ON user_id == users.id WHERE street == "6439 Zetta Hills" AND city == "Willmouth" AND state == "WY";
```
```sql
SELECT last_name,first_name,street,city,state,zip FROM addresses INNER JOIN users ON user_id == users.id WHERE users.id == (SELECT user_id FROM addresses INNER JOIN users ON user_id == users.id WHERE street == "6439 Zetta Hills" AND city == "Willmouth" AND state == "WY");
```
5. Correct Virginie Mitchell's address to "New York, NY, 10108".
```sql
UPDATE addresses SET city = "New York", zip = 10108 WHERE addresses.id == (SELECT addresses.id FROM addresses INNER JOIN users ON user_id == users.id WHERE last_name == "Mitchell" AND first_name == "Virginie" AND state == "NY");
```
6. How much would it cost to buy one of each tool? **46,477 krabby patties (or whatever monetary unit we're using)**
```sql
SELECT SUM(price) FROM items WHERE category LIKE "%tool%";
```
7. How many total items did we sell? **2,125 items**
```sql
SELECT SUM(quantity) FROM orders;
```
8. How much was spent on books? **1,081,352 krabby patties**
```sql
SELECT SUM(items.price*orders.quantity) FROM items INNER JOIN orders ON items.id == item_id WHERE category LIKE "%book%";
```
9. Simulate buying an item by inserting a User for yourself and an Order for that User. **No. ... Okay. Fine.**
```sql
INSERT INTO users (first_name, last_name, email) VALUES ("PaTrICk", "sTar","PATRICKSTAR@mrspuffsboatingschool.com");
```
```sql
INSERT INTO orders (user_id, item_id, quantity, created_at) VALUES ((SELECT id FROM users WHERE email == "PATRICKSTAR@mrspuffsboatingschool.com"), (SELECT id FROM items WHERE title == "Intelligent Rubber Chair"), 1, CURRENT_TIMESTAMP);
```
# Adventure Mode
1. What item was ordered most often? Grossed the most money? **Incredible Granite Car; and, the same.**
```sql
SELECT title FROM items WHERE id == (SELECT item_id FROM orders GROUP BY item_id ORDER BY quantity DESC, count(*) DESC LIMIT 1);
```
```sql
SELECT title FROM orders INNER JOIN items ON item_id == items.id GROUP BY item_id ORDER BY SUM(price*quantity) DESC limit 1;
```
2. What user spent the most? ****
```sql
```
3. What were the top 3 highest grossing categories? ****
```sql
```
