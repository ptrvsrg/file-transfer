# Передача файла по TCP с подсчётом скорости передачи данных

## Задание

+ Разработать TCP протокол передачи произвольного файла с одного компьютера на другой.
+ Написать клиент и сервер, реализующие этот протокол.

## Требования

### Сервер

+ В параметрах передаётся номер порта, на котором он будет ждать входящих соединений от клиентов.
+ Сервер сохраняет полученный файл в поддиректорию `uploads` своей текущей директории.
+ Сервер никогда не должен писать за пределы директории `uploads`.
+ В процессе приёма данных от клиента сервер должен раз в 3 секунды выводить в консоль мгновенную скорость приёма и
  среднюю скорость за сеанс (Под скоростью здесь подразумевается количество
  байтов переданных за единицу времени). 
+ Скорости выводятся отдельно для каждого активного клиента. Если клиент был активен менее 3
  секунд, скорость всё равно должна быть выведена для него один раз.
+ После успешного сохранения всего файла сервер проверяет, совпадает ли размер полученных данных с размером, переданным
  клиентом, и сообщает клиенту об успехе или неуспехе операции, после чего закрывает соединение.
+ Сервер должен уметь работать параллельно с несколькими клиентами. Для этого необходимо использовать потоки (POSIX
  threads или их аналог в вашей ОС).
+ Сразу после приёма соединения от одного клиента, сервер ожидает следующих клиентов.
+ В случае ошибки сервер должен разорвать соединение с клиентом. При этом он должен продолжить обслуживать остальных
  клиентов.

### Клиент

+ Клиенту передаётся в параметрах относительный или абсолютный путь к файлу, который нужно отправить.
+ Длина имени файла не превышает 4096 байт в кодировке UTF-8.
+ Размер файла не более 1 ТБ.
+ Клиенту также передаётся в параметрах DNS-имя (или IP-адрес) и номер порта сервера.
+ Клиент передаёт серверу имя файла в кодировке UTF-8, размер файла и его содержимое.
+ Клиент должен вывести на экран сообщение о том, успешной ли была передача файла.