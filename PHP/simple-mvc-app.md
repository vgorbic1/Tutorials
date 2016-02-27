## Simple MVC Application
MVC is a design pattern that suggests you organize your code in a way concerns are properly separated, and yet interact with each other in a certain fashion. **Models** fetch and mold data which is in turn sent to the **View** and therefore displayed. The **Controller** is managing the process.

## Database
Create a MySQL database `php_mvc` that contains a table `posts` with 3 columns `id`, `author` and `content`.
```sql
CREATE DATABASE php_mvc;

USE php_mvc;

CREATE TABLE posts (id INT NOT NULL AUTO_INCREMENT, author VARCHAR(255), content TEXT, PRIMARY KEY (id));
```













[SOURCE](http://requiremind.com/a-most-simple-php-mvc-beginners-tutorial/)

Application Github [repo](https://github.com/Raindal/php_mvc)
