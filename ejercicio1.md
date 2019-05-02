1 Crear una base de datos llamada call_list
""" CREATE DATABASE call_list; """

2 Conectar a base de datos
""" \c call_list """

3 En la base de datos recien creada, crear la tabla users con los campos id (clave primaria), first_name, email.
""" CREATE TABLE users( id integer PRIMARY KEY, first_name VARCHAR(50), email VARCHAR(50), ); """

4 Ingresar un usuario, llamado Carlos (el resto de los datos deben inventarlos)
""" INSERT INTO users (id, first_name, email) VALUES (1, 'Carlos', 'carlos@email.com'); """

5 Ingresar un usuario, llamada Laura (el resto de los datos deben inventarlos).
""" INSERT INTO users (id, first_name, email) VALUES (2, 'Laura', 'laura@email.com'); """

6 Crear una tabla llamada calls con los campos id (clave primaria), phone, date, user_id (foreign key relacionado a users).
""" CREATE TABLE calls( id SERIAL PRIMARY KEY, phone VARCHAR, user_id INTEGER REFERENCES users(id) ); """

7 Agregar columna date (olvidada en instrucciones)
""" ALTER TABLE calls ADD COLUMN date DATE """

8 Agregar a la tabla users el campo last_name.
""" ALTER TABLE users ADD COLUMN last_name VARCHAR; """

9 Ingresar el apellido del usuario Carlos.
""" UPDATE users SET last_name = 'Loyola' WHERE first_name = 'Carlos'; """

10 Ingresar el apellido del usuario Laura
""" UPDATE users SET last_name = 'Campos' WHERE first_name = 'Laura'; """

11 Agregar un usuario nuevo (instrucción n° 11).
""" INSERT INTO users (id, first_name, email, last_name) VALUES (3, 'Zamiz', 'zamiz@email.com','Tapellido'); """

12 Ingresar 6 llamadas asociadas al usuario Laura. (instrucción n° 9)
""" INSERT INTO calls (id, phone, user_id, date) VALUES ('1', '+569 6300 3030', 2, '2018-02-10'), ('2', '+569 6300 3030', 2, '2018-02-11'), ('3', '+569 6300 3030', 2, '2018-02-12'), ('4', '+569 6300 3030', 2, '2018-02-13'), ('5', '+569 6300 3030', 2, '2018-02-14'), ('6', '+569 6300 3030', 2, '2018-02-15'); """

13 Ingresar 4 llamadas asociadas al usuario Carlos
""" INSERT INTO calls (id, phone, user_id, date) VALUES ('7', '+569 6300 4031', 1, '2018-03-10'), ('8', '+569 6300 4030', 1, '2018-04-11'), ('9', '+569 6300 4031', 1, '2018-03-12'), ('10', '+569 6300 4030', 1, '2018-05-13'); """

14 Seleccionar la cantidad de llamados de cada uno de los usuarios (nombre de usuario y cantidad de llamadas)
""" SELECT first_name, count(*) FROM users, calls WHERE calls.user_id = users.id group by first_name; """

15 Seleccionar los llamados del usuario llamado Carlos ordenados por fecha en orden descendente.
""" SELECT phone, date FROM users, calls WHERE calls.user_id = users.id and user_id = 1 ORDER BY date DESC; """

16 Necesito agregar a la base una tabla de auditoría que registre el motivo del borrado de una llamada y el usuario que lo efectuó.
""" CREATE TABLE audit( id SERIAL PRIMARY KEY, delete_reason VARCHAR, user_id INTEGER REFERENCES users(id) ); """

17 Agregar id de llamada
""" ALTER TABLE audit ADD COLUMN call_id INTEGER REFERENCES calls(id); """

18 Quitar user_id (se puede obtener por el call_id)
""" ALTER TABLE audit DROP COLUMN user_id; """