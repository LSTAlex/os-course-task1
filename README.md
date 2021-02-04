os-course-task1
# Операционные системы. Лабораторная работа №1: работа с текстовыми потоками в командном интерпретаторе Bash

## Цель работы
Изучение принципов работы с командным интерпретатором GNU/Linux и основ обработки текстовых файлов с помощью команд `grep`, `awk`, `sed`.

## Справочный материал
Справочный материал по командному интерпретатору bash приведен в файле [bash_help.pdf](bash_help.pdf). Посмотреть документацию к интересующей команде командного интерпретатора можно выполнив в консоли `man <имя_команды>`.

## Задание на лабораторную работу
1. Подготовить операционную систему GNU/Linux к работе. При необходимости, воспользоваться средством виртуализации VMware Workstation/Player, Oracle VirtualBox или др. В качестве дистрибутива рекомендуется взять [Ubuntu](https://www.ubuntu.com/download/desktop).
2.	Создать в домашней директории пользователя `/home/user/` каталог `lab1` с помощью команды `mkdir`. Перейти в этот каталог с помощью команды `cd`. Всю дальнейшную работу вести внутри этого каталога.
3.  С помощью команды `git clone <путь_к_репозиторию_на_github>` создать локальную копию репозитория. Перейти в каталог с копией репозитория (при клонировании репозитория каталог будет иметь такое же название, как и сам репозиторий на github.com).
4.	Отправить на электронную почту k43guap@ya.ru следующую информацию: номер группы, ФИО и свое имя пользователя на github.com. Письмо должно содержать ровно три строки, в первой строке - номер группы, во второй - ФИО (полностью), в третьей - имя пользователя на github.com. Тема письма должна содержать текст `OS` или `Operating systems`.
5.	Ознакомиться с форматом файла `dns-tunneling.log` и хранящимися в нем данными с помощью команд `cat`, `head`, `tail`, `more`, `less` и т.п.
6.	Подсчитать количество записей в файле `dns-tunneling.log`.
7.	Вычислить номер варианта задания как остаток от деления порядкового номера студента по списку в журнале на количество вариантов заданий. Если остаток равен нулю, необходимо брать последнее задание.
8.  Объявить в файле `lab1.sh` переменную `TASKID`, указав в качестве ее значения номер варианта задания в виде целого числа.
9.  Объявить в файле `lab1.sh` переменную `VAR_1`, указав в качестве ее значения количество записей в файле `dns-tunneling.log` (данное значение должно вычисляться динамически во время выполнения скрипта).
10.	Дописать в файл `lab1.sh` код для обработки данных из файла `dns-tunneling.log` в соответствии с вариантом задания используя исключительно команды командного интерпретатора `bash`. Использовать другие интерпретируемые или компилируемые языки запрещается. Скрипт должен читать файл `dns-tunneling.log` и все результаты должны вычисляться на его основе в реальном времени, использовать в скрипте заранее полученные значения запрещается.
11.	Сделать файлы `lab1.sh` и `test.sh` исполняемыми с помощью команды `chmod`.
12.	Отладить скрипт `lab1.sh` и убедиться, что тесты из `test.sh` выполняются без ошибок. Следует иметь в виду, что в случае принудительного прерывания выполнения тестов (например, командой Ctrl+C с клавиатуры, или путем выключения питания компьютера) следует самостоятельно восстановить файл `dns-tunneling.log` из бэкапа командой `mv dns-tunneling.log.bak dns-tunneling.log` или `git checkout HEAD dns-tunneling.log`.
13.	С помощью команд `git add lab1.sh`, `git commit` и `git push` добавить файл с написанным кодом в репозиторий. Убедиться, что тест в репозитории пройден успешно.
14.	Подготовить и защитить отчет о выполнении лабораторной работы.


## Описание текстовых данных
Файл `dns-tunneling.log` содержит логи [DNS-сервера](https://ru.wikipedia.org/wiki/DNS), представленные в виде текстового файла, в котором каждая строка соответствует записи о поступившем на вход сервера запросе. В логах сохраняются следующие параметры запроса, разделенные символом табуляции:

1.	Название провайдера телекоммуникационных услуг: `character array`,
2.	Название узла, на котором хранятся данные: `character array`,
3.	Порядковый номер запроса: `long`,
4.	Отметка времени, когда поступил запрос: два числа `long`, разделенных точкой; первое число – количество секунд, прошедших  с 1 января 1970 года; второе число – количество микросекунд; т.е. фактически это тип данных `float`,
5.	IP-адрес пользователя: `character array`,
6.	Порт пользователя: `int`,
7.	Локальный IP-адрес, на который поступил запрос: `character array`,
8.	Локальный порт: `int`,
9.	Название оборудования DNS-сервера: `character array`,
10.	Класс запроса: `int`,
11.	[Тип запроса](https://ru.wikipedia.org/wiki/Типы_ресурсных_записей_DNS): `int`,
12.	Код возвращаемого значения: `int`,
13.	Флаги: `int`,
14.	Вспомогательный идентификатор: `int`,
15.	Запрашиваемый URL: `character array`,
16.	Зона: `character array`,
17.	Вспомогательное поле 1: `character array`,
18.	Вспомогательное поле 2: `character array`,
19.	Вспомогательное поле 3: `character array`,
20.	Вспомогательное поле 4: `character array`,
21.	Ответ сервера: `character array`,
22.	Вспомогательное поле 5: `character array`,
23.	Вспомогательное поле 6: `character array`,
24.	Длина ответа: `int`

## Варианты заданий

Во всех вариантах предполагается, что в конце каждой строки с текстом стоит символ перевода строки `\n`, а пустые строки отсутствуют.  

1.	Написать скрипт с использованием grep, sed, awk (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат XML со следующей структурой:
```
<dnslog>
<row>
    <serial>Порядковый номер запроса</serial>
    <client_ip>IP адрес пользователя</client_ip>
    <url>Запрашиваемый URL</url>
</row>
<row>
    <serial>Порядковый номер запроса</serial>
    <client_ip>IP адрес пользователя</client_ip>
    <url>Запрашиваемый URL</url>
</row>
<row>
    ...
</row>
</dnslog>
```
Текст внутри тегов `<serial>`, `<client_ip>` и `<url>` необходимо заменить соответствующими значениями из логов. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция). Сохранить в файле `results.txt` результат применения написанного скрипта к последним 15 строкам файла `dns-tunneling.log`.  
В переменную `VAR_2` записать количество записей в получившемся текстовом файле, которые содержат обращение к любым поддоменам `1yf.de.` и `2yf.de.`.

2.	Написать скрипт с использованием grep, sed, awk (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат XML со следующей структурой:
```
<dnslog>
<row>
    <timestamp>Отметка времени, когда поступил запрос</timestamp>
    <client_ip>IP адрес пользователя</client_ip>
    <client_port>Порт пользователя</client_port>
</row>
<row>
    <timestamp>Отметка времени, когда поступил запрос</timestamp>
    <client_ip>IP адрес пользователя</client_ip>
    <client_port>Порт пользователя</client_port>
</row>
<row>
    ...
</row>
</dnslog>
```
Текст внутри тегов `<timestamp>`, `<client_ip>` и `<client_port>` необходимо заменить соответствующими значениями из логов. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция). Сохранить в файле `results.txt` результат применения написанного скрипта к первым 20 строкам файла `dns-tunneling.log`.  
В переменную `VAR_2` записать количество записей в получившемся текстовом файле, которые содержат запросы от пользователей с IP-адресами из подсети `10.1.*.*`.

3.	Сформировать список IP-адресов пользователей, присутствующих в логах, убрать повторы, отсортировать список в порядке увеличения IP-адреса и сохранить в файле `results.txt`. В переменную `VAR_2` записать количество запросов, пришедших с IP-адреса пользователя, оказавшегося вторым в файле `results.txt`.
4.	Вывести на экран в формате `"ГГГГ-MM-ДД ЧЧ:мм:СС.нс"` дату и время поступления самого раннего и самого позднего DNS-запросов, где `ДД` – день, `ММ` – месяц, `ГГГГ` – год, `ЧЧ` – час, `мм` – минуты, `СС` – секунды, `нс` – наносекунды. Для этого воспользоваться командой `date` с флагом `–d`, например: `date -d @946684800`. Время и дату преобразовать в часовой пояс всемирного координированного времени (UTC). Сохранить указанные две даты в файл `results.txt`, каждую на новой строке. При выполнении задания в MacOS рекомендуется использовать утилиту `gdate` (GNU date) вместо `date`. При обработке данных исходить из того, что записи в логе могут быть не отсортированы в порядке увеличения отметки времени.  
В переменную `VAR_2` записать количество запросов, пришедших с того же IP-адреса пользователя, что и самый ранний найденный запрос.
5.	Найти количество запросов, поступивших за первую, вторую, третью и четвертую секунды ведения лога. Сохранить получившиеся четыре числа в файл `results.txt`. При обработке данных исходить из того, что записи в логе могут быть не отсортированы в порядке увеличения отметки времени.
В переменную `VAR_2` записать порт пользователя, с которого поступил самый ранний найденный запрос.
6.	Найти все [доменные имена второго уровня](https://ru.wikipedia.org/wiki/Доменное_имя_второго_уровня) (включая домен верхнего уровня), к которым обращались пользователи за все время ведения лога. Подсчитать количество запросов каждого из доменных имен второго уровня (включая их поддомены). Предварительно все доменные имена привести к нижнему регистру. В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:
`<доменное имя второго уровня><символ табуляции><количество запросов этого доменного имени>`
Строки в файле отсортировать в порядке убывания числа запросов к доменам второго уровня. Если число запросов к нескольким доменам второго уровня одинаковое, отсортировать их по имени домена в алфавитном порядке.  
В переменную `VAR_2` записать количество строк в получившемся файле `results.txt`.
7.	Подсчитать количество обращений к доменам `whatsapp.net.` и `google.com.`. Найти суммарный объем DNS-трафика к каждому из этих доменов. Объем трафика в одном DNS-запросе равен количеству символов, из которых состоит запрашиваемое имя, включая все поддомены и точки. Найти самый длинный запрошенный URL за все время ведения лога, не ограничиваясь доменами `whatsapp.net.` и `google.com.`. Если URL максимальной длины несколько, взять первый из них по порядку появления в логах. Сформировать файл `results.txt` из трех строк в следующем виде:
```
<самый длинный запрошенный URL>
whatsapp.net.;<количество обращений к whatsapp.net.>;<суммарный объем DNS-трафика к whatsapp.net.>
google.com.;<количество обращений к google.com.>;<суммарный объем DNS-трафика к google.com.>
```  
В переменную `VAR_2` записать суммарный объем DNS-трафика к `google.com.`.

8.	Написать скрипт с использованием `grep`, `sed`, `awk` (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат JSON со следующей структурой:
```
{
    "dnslog": [
        "entry": {
            "timestamp": "Отметка времени, когда поступил запрос",
            "client ip": "IP адрес пользователя",
            "url": "Запрашиваемый URL"
        },
        "entry": {
            "timestamp": "Отметка времени, когда поступил запрос",
            "client ip": "IP адрес пользователя",
            "url": "Запрашиваемый URL"
        },
        ...
    ]
}
```
Взятый в кавычки русский текст необходимо заменить соответствующими значениями из логов. В формате JSON необходимо все ключи и все строковые значения помещать в двойные кавычки, числовые же значения (int, float) следует вставлять без кавычек. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция).
Сохранить в файле `results.txt` результат применения написанного скрипта к строкам с 15 по 30-ю (включительно) файла `dns-tunneling.log`.  
В переменную `VAR_2` записать количество записей в получившемся текстовом файле, которые содержат обращение к любым поддоменам `1yf.de.` и `2yf.de.`.

9.	Написать скрипт с использованием `grep`, `sed`, `awk` (необходимо использовать не менее одной из указанных утилит; использовать все три необязательно) для переконвертирования данных в формат JSON со следующей структурой:
```
{
    "Порядковый номер запроса": {
        "timestamp": "Отметка времени, когда поступил запрос",
        "client ip": "IP адрес пользователя",
        "client port": "Порт пользователя"
    },
    "Порядковый номер запроса": {
        "timestamp": "Отметка времени, когда поступил запрос",
        "client ip": "IP адрес пользователя",
        "client port": "Порт пользователя"
    },
    ...
}
```
Взятый в кавычки русский текст необходимо заменить соответствующими значениями из логов. В формате JSON необходимо все ключи и все строковые значения помещать в двойные кавычки, числовые же значения (int, float) следует вставлять без кавычек. Для отступов использовать символ табуляции (4 пробела в примере выше = одна табуляция).
Сохранить в файле `results.txt` результат применения написанного скрипта к строкам с 30 по 50-ю (включительно) файла `dns-tunneling.log`.  
В переменную `VAR_2` записать количество записей в получившемся текстовом файле, которые содержат запросы от пользователей с IP-адресами из подсети `10.1.*.*`.

10.	Домены [второго уровня](https://ru.wikipedia.org/wiki/Доменное_имя_второго_уровня) `1yf.de.` и `2yf.de.` являются DNS-туннелями. Они используются для передачи трафика по DNS-протоколу в обход HTTP (например, для обхода блокировок). Подсчитать количество обращений к каждому из доменов второго уровня `1yf.de.` и `2yf.de.` (сюда входят и обращения ко всем их поддоменам). Вычислить среднее количество запросов в секунду по всем DNS-туннелям за первые полчаса ведения логов, округлить до трех знаков после запятой (разделитель целой и дробной части - точка). Сохранить полученные числа в файле `results.txt` по одному на строку: первая строка - количество обращений к домену `1yf.de.`, вторая строка - количество обращений к `2yf.de.`, третья строка - среднее количество запросов к `1yf.de.` и `2yf.de.` за первые полчаса. Необходимо помнить, что записи в файле `dns-tunneling.log` могут идти в произвольном порядке.  
В переменную `VAR_2` записать среднее количество запросов в секунду по всем DNS-туннелям за первые полчаса ведения логов.
11.	Подсчитать количество уникальных пользователей, использующих DNS-туннели (см. предыдущий вариант). Пользователей можно идентифицировать по их IP-адресам. Определить количество DNS–запросов, выполненных каждым из найденных пользователей. В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:
`<IP-адрес><символ табуляции><количество запросов с использованием DNS-туннелей, выполненных с указанного IP-адреса>`  
Строки в файле отсортировать в порядке убывания числа запросов к доменам DNS-туннелей. Пользователей с одинаковым количеством запросов дополнительно отсортировать по возрастанию IP-адреса. Для этого можно, например, использовать повторную сортировку с ключом `-s` или `--stable`.  
В переменную `VAR_2` записать количество строк в файле `results.txt`.

12.	Вычислить в процентах, какое количество DNS-запросов в приведенном логе приходится на DNS-туннели с разбивкой на `1yf.de.` и `2yf.de.` (см. предыдущие варианты), а также домены `whatsapp.net.` и `google.com.`. Получившиеся числа округлить до 3 знаков после запятой и записать в формате с плавающей запятой (разделитель целой и дробной части - точка) в файл `results.txt` по одному на строку. Порядок следования чисел должен быть такой же, как указано в задании.
В переменную `VAR_2` записать общее количество DNS-запросов к `google.com.`, включая поддомены.

13. Подсчитать количество DNS-запросов всех типов. В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:  
`<тип запроса>;<количество запросов этого типа>`  
Строки в файле отсортировать в порядке убывания числа запросов разных типов. Если количество запросов двух разных типов одинаковое, отсортировать их по номеру типа запроса в порядке возрастания.  
В переменную `VAR_2` записать количество запросов [`MX`](https://ru.wikipedia.org/wiki/Запись_MX) (код данного типа запроса равен 15) в получившемся файле `results.txt`.

14. Найти все DNS-запросы типа `A` (код типа запроса равен 1). В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:  
`<доменное имя, к которому обращен запрос типа A><символ табуляции><количество запросов этого доменного имени>`  
Строки в файле отсортировать в порядке убывания числа запросов к доменам. Если число запросов к нескольким доменам  одинаковое, отсортировать их по имени домена в алфавитном порядке. Предварительно все доменные имена привести к нижнему регистру.  
В переменную `VAR_2` записать количество строк в получившемся файле `results.txt`.

15. Найти все DNS-запросы к несуществующим доменам - [`NXDOMAIN`](http://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) (код возвращаемого значения равен 3). Найти все уникальные IP-адреса пользователей, с которых поступали DNS-запросы к несуществующим доменам, и подсчитать количество таких запросов от каждого из пользователей, сделавших хотя бы один подобный запрос. В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:  
`<IP-адрес пользователя, сделавшего хотя бы один запрос к несуществующему домену><символ табуляции><количество запросов к несуществующим доменам от этого пользователя>`  
Строки в файле отсортировать в порядке убывания числа запросов. Пользователей с одинаковым количеством запросов дополнительно отсортировать по возрастанию IP-адреса. Для этого можно, например, использовать повторную сортировку с ключом `-s` или `--stable`.  
В переменную `VAR_2` записать количество строк в файле `results.txt`.

16. Среди всех успешных DNS-запросов - [`No Error`](http://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-6) (код возвращаемого значения равен 0) - подсчитать количество запросов каждого типа, см. поле "тип запроса". В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:  
`<тип запроса><символ табуляции><количество успешных запросов этого типа>`  
Строки в файле отсортировать в порядке убывания числа запросов разных типов. Если количество запросов двух разных типов одинаковое, отсортировать их по номеру типа запроса в порядке возрастания.  
В переменную `VAR_2` записать количество запросов [`AAAA`](http://www.iana.org/assignments/dns-parameters/dns-parameters.xhtml#dns-parameters-4) (код данного типа запроса равен 28) в получившемся файле `results.txt`.

17. Найти всех пользователей, посылавших DNS-запросы c нечетных портов с номером меньше `40000`. Сохранить в файле `results.txt` список IP-адресов этих пользователей по одному адресу в каждой строке, отсортировав их в порядке возрастания IP-адреса.  
В переменную `VAR_2` записать количество запросов, пришедших на DNS-сервер `10.208.61.116` с IP-адреса, оказавшегося на второй строке в файле `results.txt`.

18. Найти всех пользователей, отправлявших запросы с четных портов в диапазоне от `1900` до `2000` не включая их. Вывести в файл `results.txt` таблицу, в которой каждая строка имеет вид:  
`<IP-адрес пользователя><символ табуляции><порт пользователя><символ табуляции><количество запросов с этого порта>`  
Строки в файле отсортировать в порядке убывания числа запросов. Если количество запросов одинаковое, отсортировать по IP-адресу в порядке возрастания. В случае совпадения количества запросов и IP-адреса пользователя, дополнительно отсортировать по номеру порта в порядке его возрастания. Для этого можно, например, использовать повторную сортировку с ключом `-s` или `--stable`.  
В переменную `VAR_2` записать количество запросов, пришедших на с IP-адреса, оказавшегося последним в файле `results.txt`.

19. Среди последних 200 строк в файле `dns-tunneling.log` найти те, запрашиваемый URL которых начинается на `aD`. Отсортировать все найденные уникальные запрашиваемые URL по алфавиту и записать их в файл `results.txt`.
В переменную `VAR_2` записать количество символов в самой короткой строке в файле `results.txt`.

20. Найти все доменные имена [второго уровня](https://ru.wikipedia.org/wiki/Доменное_имя_второго_уровня), находящиеся в доменной зоне `net.`. Подсчитать количество запросов к каждому из найденных доменов второго уровня, включая его поддомены. В файл `results.txt` вывести таблицу, в которой каждая строка имеет вид:  
`<доменное имя><символ табуляции><количество запросов этого доменного имени>`  
Строки в файле отсортировать в порядке убывания числа запросов к доменам. Если число запросов к нескольким доменам  одинаковое, отсортировать их по имени домена в алфавитном порядке. Предварительно все доменные имена привести к нижнему регистру.  
В переменную `VAR_2` записать количество запросов к домену второго уровня, оказавшемуся на третьей строке в файле `results.txt`.

## Содержание отчета

1.	Титульный лист 
2.	Цель работы
3.	Индивидуальное задание
4.	Описание входных данных
5.	Результат выполнения работы
6.	Исходный код программы с комментариями
7.	Выводы
