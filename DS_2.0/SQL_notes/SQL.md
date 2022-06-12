### Задание 1.1
>Напишите запрос, который выведет из таблицы kinopoisk столбцы с названием фильма, годом его выпуска и рейтингом.

``` sql
SELECT /*выбор столбцов*/
movie_title, /*столбец movie_title*/
2020 - year, /*столбец, каждое из значений которого ровно разнице 2020 и соответствующего значения столбца year*/
rating /*столбец rating*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
```
---
### Задание 1.2

>Напишите запрос, который выведет из таблицы kinopoisk следующие столбцы:
имя режиссёра (director),
название фильма (movie_title),
разница между максимально возможным рейтингом (10) и рейтингом этого фильма.

``` sql
SELECT /*выбрать столбцы*/
director, /*столбец director*/
movie_title, /*столбец movie_title*/
10 - rating AS difference /*столбец, значения в котором равны разнице 10 и каждого соответствующего значения столбца rating; присвоить столбцу алиас difference*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
``` 
___

## ПРОСТЫЕ ОПЕРАЦИИ С ДАННЫМИ

>Со столбцами, которые содержат числовые данные, можно проводить арифметические операции:
* сложение с помощью + ;
* вычитание с помощью ;
* умножение с помощью * ;
* деление с помощью / ;

### Задание 1.3
>Напишите запрос, который выведет столбцы с именем режиссёра, названием фильма, рейтингом по 100-балльной шкале (столбец rating_100).

Рейтинг по 100-балльной шкале определите как оценку по 10-балльной, умноженную на 10.
``` sql
SELECT /*выбрать столбцы*/
    movie_title, /*столбец movie_title*/
    year / rating /*столбец, значения которого равны результату деления значений столбца year на соответствующие значения столбца rating*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
```
---

``` sql
SELECT /*выбор*/
year, /*столбец year*/
movie_title, /*столбец movie_title*/
director /*столбец director*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
WHERE (rating > 8.5 AND year < 2000) /*при условии, что рейтинг больше 8.5 и год создания до 2000*/
OR year >= 2000 /*или год создания — 2000 и позднее*/
```

### Задание 2.4
> Напишите запрос, который выводит названия фильмов, вышедших в прокат в 2000, 1985 и 1939 годах.

``` sql
SELECT movie_title
FROM sql.kinopoisk
WHERE year in (2000,1985,1939)
```
---

``` sql
SELECT * /*выбор всех полей*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
WHERE movie_title LIKE 'А%' /*если название фильма начинается на А*/
```

### Задание 2.5
>Напишите запрос, чтобы вывести название и год выпуска в прокат тех фильмов, которые были сняты режиссёром по имени Дэвид (то есть значение в поле director начинается с 'Дэвид') и имеют рейтинг больше 8.

``` sql
SELECT movie_title,year
FROM sql.kinopoisk
WHERE director like 'Дэвид%' and rating>8
```

### Задание 3.2
>Напишите запрос, который выведет столбцы с названием фильма, его описанием и годом выхода в прокат. Оставьте только те фильмы, у которых рейтинг не ниже 8.2 и страна производства — не США.
>Отсортируйте вывод по году выхода фильма в порядке убывания.

``` sql
SELECT movie_title,overview,year
FROM sql.kinopoisk
WHERE country != 'США'
AND rating >8.2 
ORDER BY year DESC
```

---
``` sql
SELECT /*выбор*/
director, /*столбец director*/
movie_title, /*столбец movie_title*/
year /*столбец year*/
FROM sql.kinopoisk /*из таблицы sql.kinopoisk*/
ORDER BY 1, 3 DESC /*сортировка по первому и третьему столбцам*/
```

``` sql
SELECT
столбец1 AS новое_название,
столбец2,
столбец3
FROM таблица
WHERE (условие1 OR условие2)
AND условие3
ORDER BY сортировка1, сортировка2
OFFSET 1 LIMIT 2
```

### Задание 5.3

>Напишите запрос, который выводит столбцы «Название фильма» (movie_title), «Режиссёр» (director), «Сценарист» (screenwriter), «Актёры» (actors). Оставьте только те фильмы, у которых:

>рейтинг между 8 и 8.5 (включительно) ИЛИ год выхода в прокат до 1990;
есть описание;
название начинается не с буквы 'Т';
название состоит ровно из 12 символов.
Оставьте только ТОП-7 по рейтингу.
>
``` sql
SELECT
movie_title as "Название фильма",
director as "Режиссёр",
screenwriter as "Сценарист",
actors as "Актёры"
FROM sql.kinopoisk
where (rating between 8 and 8.5 or year <1990)
AND overview is not null
AND movie_title not like 'T%'
AND LENGTH(movie_title) =12

ORDER BY rating desc
limit 7
```

---
``` sql
SELECT /*выбор*/
COUNT(*) AS "всего травяных покемонов", /*подсчёт всех строк; назначить алиас "всего травяных покемонов"*/
COUNT(type2) AS "покемонов с дополнительным типом", /*подсчёт непустых строк в столбце type2; назначить алиас "покемонов с дополнительным типом"*/
AVG(attack) AS "средняя атака", /*среднее значение столбца attack; назначить алиас "средняя атака"*/
AVG(defense) AS "средняя защита" /*среднее значение столбца defense; назначить алиас "средняя защита"*/
FROM sql.pokemon /*из таблицы sql.pokemon*/
WHERE type1 = 'Grass'/*при условии, что значение столбца type1 содержит grass*/
```


### Задание 3.5

``` sql
SELECT
COUNT(*) pokemon_count,
AVG(speed) avg_speed,
MAX(hp) max_hp,
MIN(hp) min_hp
FROM sql.pokemon
WHERE type1 = 'Electric'
AND type2 IS NOT NULL
AND (attack > 50 OR defense > 50)
```
---
### Задание 4.1
>Напишите запрос, который выведет:

>число различных дополнительных типов (столбец additional_types_count);
среднее число очков здоровья (столбец avg_hp);
сумму показателей атаки (столбец attack_sum) в разбивке по основным типам (столбец primary_type).
Отсортируйте результат по числу дополнительных типов в порядке убывания, при равенстве — по основному типу в алфавитном порядке.
Столбцы к выводу (обратите внимание на порядок!): primary_type, additional_types_count, avg_hp, attack_sum.
> 
``` sql
SELECT
   type1 primary_type,
   count(DISTINCT type2) additional_types_count,
   AVG(hp) avg_hp,
   SUM(attack) attack_sum
FROM sql.pokemon
GROUP BY primary_type
ORDER BY 2 DESC, 1
```

### Задание 5.1

>Напишите запрос, который выведет основной и дополнительный типы покемонов (столбцы primary_type и additional_type) для тех типов, у которых средний показатель атаки больше 100 и максимальный показатель очков здоровья меньше 80.

``` sql
SELECT
    type1 AS primary_type,
    type2 AS additional_type
    
FROM sql.pokemon
GROUP BY primary_type, additional_type
HAVING AVG(attack) > 100
and max(hp)<80
```
---


``` sql
SELECT
столбец1 AS новое_название,
столбец2,
АГРЕГАТ(столбец3)
FROM таблица
WHERE (условие1 OR условие2)
AND условие3
GROUP BY столбец1, столбец2
HAVING АГРЕГАТ(столбец3) > 5
ORDER BY сортировка1, сортировка2
OFFSET 1 LIMIT 2
```
---

### Задание 6.1

>Сколько различных значений показателей атаки есть у покемонов с типом Water (основным или дополнительным)?
>
``` sql
SELECT 
   COUNT(distinct attack) AS pokemon_count 
FROM sql.pokemon 
where type2 = 'Water'
OR type1 = 'Water'
```
---

### Задание 6.2
> Напишите запрос, который выведет основной и дополнительный типы покемонов и средние значения по каждому показателю (столбцы avg_hp, avg_attack, avg_defense, avg_speed).
Оставьте только те пары типов, у которых сумма этих четырёх показателей более 400.

``` sql
SELECT 
 type1 AS primary_type,
 type2 AS additional_type,
 AVG(hp) as avg_hp,
 AVG(attack) as avg_attack,
 AVG(defense) as avg_defense,
 AVG(speed) as avg_speed
FROM sql.pokemon 
GROUP BY 1, 2
HAVING AVG(hp) + AVG(attack) + AVG(defense) + AVG(speed) > 400
```

### Задание 6.3
>Напишите запрос, который выведет столбцы с основным типом покемона и общим количеством покемонов этого типа.
>Учитывайте только тех покемонов, у которых или показатель атаки, или показатель защиты принимает значение между 50 и 100 включительно.
>Оставьте только те типы покемонов, у которых максимальный показатель здоровья не больше 125.
>Выведите только тот тип, который находится на пятом месте по количеству покемонов.
>
``` sql
SELECT
type1 AS primary_type,
count(*)

FROM sql.pokemon
where attack between 50 and 100 or defense between 50 and 100
GROUP BY 1

having max(hp)<=125
ORDER BY COUNT(*) DESC
LIMIT 1 offset 4
```