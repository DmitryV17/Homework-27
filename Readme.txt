Это проект консольного чата с использованием базы данных MySQL, котоаря используется как сервер. При работе с ней подразумевается 
что уже создана база данныых "Console_chat", если же ее нет то вот инструкция как ее создать:
1. На сервере базы данных создайте новую базу данных и выберите её:
   CREATE DATABASE Console_chat;
   USE DATABASE Console_chat;
2. Теперь нужно создать таблицу с данными пользователей:
   CREATE TABLE user(id_user INT AUTO_INCREMENT PRIMARY KEY, login_user VARCHAR(255) NOT NULL, password_user VARCHAR(255), name_user VARCHAR(255), email_user VARCHAR(255));
   При желании наполнить несколькими примерами по шаблону:
   INSERT INTO user(id_user, login_user, password_user, name_user, email_user) values(default, 'Login', 'Password', 'Name', 'Email'));
3. Создаем вторую таблицу с сообщениями пользователей:
   CREATE TABLE message(id_message INT AUTO_INCREMENT PRIMARY KEY, sender INT, recipient INT, text_message TEXT, time_message TIMESTAMP NOT NULL );
   И два внешних ключа на id пользователей для отправтителей и получателей сообщений:
   ALTER TABLE message ADD FOREIGN KEY(sender) REFERENCES user(id_user);
   ALTER TABLE message ADD FOREIGN KEY(recipient) REFERENCES user(id_user);
   При желании заполняем вторую таблицу примерами по шаблону:
   INSERT INTO message(id_message, sender, recipient, text_message, time_message) values(default, 1, 2, 'Text message', NOW());
   
Теперь база данных готова к работе. Осталось настроить Visual Studio для работы с сервером MySQL:
   Запустите среду разработки Microsoft Visual C++ и создайте новый пустой проект "Консольное приложение Windows».
   Далее нужно открыть страницу свойств (Property Pages) с помощью главного меню (Проект->Свойства).
   В окне страницы свойств сначала добавьте к параметру "Дополнительные каталоги включаемых файлов" (Свойства конфигурации->С/С++->Общие) строку "C:\Program Files\MySQL\MySQL Server 8.0\include".
   Затем — к параметру "Дополнительные каталоги библиотек" (Свойства конфигурации->Компоновщик->Общие) строку "C:\Program Files\MySQL\MySQL Server 8.0\lib".
   Далее к параметру "Дополнительные зависимости" (Свойства конфигурации->Компоновщик->Ввод) добавьте значения libmysql.lib:

   Теперь можно использовать клиент консольного чата для работы с сервером MySQL
