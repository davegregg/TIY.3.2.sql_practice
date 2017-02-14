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

SELECT last_name,first_name,street,city,state,zip FROM addresses INNER JOIN users ON user_id == users.id WHERE users.id == (SELECT user_id FROM addresses INNER JOIN users ON user_id == users.id WHERE street == "6439 Zetta Hills" AND city == "Willmouth" AND state == "WY");
```
5. Correct Virginie Mitchell's address to "New York, NY, 10108".
```sql
```
6. How much would it cost to buy one of each tool?
```sql
```
7. How many total items did we sell?
```sql
```
8. How much was spent on books?
```sql
```
9. Simulate buying an item by inserting a User for yourself and an Order for that User.
```sql
```