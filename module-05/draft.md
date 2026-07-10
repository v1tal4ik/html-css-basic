# Таблиці

# Табличні дані. Розмітка таблиць

Таблиця — елемент для відображення структурованих даних у рядках та стовпцях.

<table class="schedule-table">
  <tr>
    <td>HTML</td>
    <td>Mon</td>
    <td>10:00</td>
  </tr>
  <tr>
    <td>CSS</td>
    <td>Wed</td>
    <td>12:00</td>
  </tr>
  <tr>
    <td>JavaScript</td>
    <td>Fri</td>
    <td>14:00</td>
  </tr>
</table>

Базова структура:

- <table> — контейнер таблиці
- <tr> — рядок таблиці (table row)
- <td> — клітинка з даними (table data)

.schedule-table {
border-collapse: collapse;
width: 100%;
}

.schedule-table td {
padding: 12px 16px;
border: 1px solid rgba(46, 47, 66, 0.2);
}

## Важливо

- Таблиці — тільки для табличних даних (розклади, прайси, статистика). НЕ для верстки layout.
- <tr> — завжди прямий нащадок <table> (або thead/tbody/tfoot).
- <td> — завжди прямий нащадок <tr>.
- Кількість <td> у кожному <tr> повинна бути однаковою (або компенсована colspan).
- border-collapse: collapse — прибирає подвійні рамки між клітинками.

---

# Клітинки-заголовки. Заголовки стовпців

Елемент <th> — клітинка-заголовок. Текст жирний та центрований за замовчуванням.

<!-- 🆕 th — заголовки стовпців у першому рядку -->
<table class="schedule-table">
  <tr>
    <th>Course</th>
    <th>Day</th>
    <th>Time</th>
  </tr>
  <tr>
    <td>HTML</td>
    <td>Mon</td>
    <td>10:00</td>
  </tr>
  <tr>
    <td>CSS</td>
    <td>Wed</td>
    <td>12:00</td>
  </tr>
  <tr>
    <td>JavaScript</td>
    <td>Fri</td>
    <td>14:00</td>
  </tr>
</table>

.schedule-table th {
padding: 12px 16px;
border: 1px solid rgba(46, 47, 66, 0.2);
background-color: #f4f4fd;
text-align: left;
font-weight: 600;
}

## Важливо

- <th> замість <td> — семантично позначає заголовок (для скрінрідерів та SEO).
- За замовчуванням текст у <th> жирний (font-weight: bold) та центрований (text-align: center).
- text-align: left — якщо потрібно вирівняти заголовки по лівому краю.
- <th> може бути заголовком стовпця (у першому рядку) або заголовком рядка (у першій клітинці).

---

# Клітинки-заголовки. Заголовок рядка

<th> у першій клітинці рядка — позначає заголовок цього рядка.

<!-- 🆕 th у першій клітинці кожного рядка — заголовок рядка -->
<table class="schedule-table">
  <tr>
    <th>Course</th>
    <th>Day</th>
    <th>Time</th>
  </tr>
  <tr>
    <th>HTML</th>
    <td>Mon</td>
    <td>10:00</td>
  </tr>
  <tr>
    <th>CSS</th>
    <td>Wed</td>
    <td>12:00</td>
  </tr>
  <tr>
    <th>JavaScript</th>
    <td>Fri</td>
    <td>14:00</td>
  </tr>
</table>

## Важливо

- <th> у рядку — семантично вказує що ця клітинка є заголовком для решти даних у рядку.
- Можна мати <th> і в першому рядку (заголовки стовпців) і в першій клітинці (заголовки рядків) одночасно.
- Для уточнення ролі заголовка використовується атрибут scope.

---

# Атрибут scope

Атрибут scope — вказує до чого відноситься заголовок: до стовпця чи до рядка.

<!-- 🆕 scope="col" та scope="row" -->
<table class="schedule-table">
  <tr>
    <th scope="col">Course</th>
    <th scope="col">Day</th>
    <th scope="col">Time</th>
    <th scope="col">Room</th>
  </tr>
  <tr>
    <th scope="row">HTML</th>
    <td>Mon</td>
    <td>10:00</td>
    <td>101</td>
  </tr>
  <tr>
    <th scope="row">CSS</th>
    <td>Wed</td>
    <td>12:00</td>
    <td>102</td>
  </tr>
  <tr>
    <th scope="row">JavaScript</th>
    <td>Fri</td>
    <td>14:00</td>
    <td>103</td>
  </tr>
</table>

Значення scope:

- scope="col" — заголовок стовпця
- scope="row" — заголовок рядка
- scope="colgroup" — заголовок групи стовпців
- scope="rowgroup" — заголовок групи рядків

## Важливо

- scope покращує доступність — скрінрідер правильно зв'язує заголовок з даними.
- scope="col" — для <th> у першому рядку (заголовки стовпців).
- scope="row" — для <th> у першій клітинці рядка (заголовки рядків).
- Візуально scope нічого не змінює — це чисто семантичний атрибут.
- Рекомендується завжди вказувати scope для складних таблиць.

---

# Розділи таблиці

Елементи <thead>, <tbody>, <tfoot> — семантичне розділення таблиці на шапку, тіло та підвал.

<!-- 🆕 thead, tbody, tfoot -->
<table class="schedule-table">
  <thead>
    <tr>
      <th scope="col">Course</th>
      <th scope="col">Day</th>
      <th scope="col">Time</th>
      <th scope="col">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">HTML</th>
      <td>Mon</td>
      <td>10:00</td>
      <td>2000 UAH</td>
    </tr>
    <tr>
      <th scope="row">CSS</th>
      <td>Wed</td>
      <td>12:00</td>
      <td>2500 UAH</td>
    </tr>
    <tr>
      <th scope="row">JavaScript</th>
      <td>Fri</td>
      <td>14:00</td>
      <td>4000 UAH</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td></td>
      <td></td>
      <td>8500 UAH</td>
    </tr>
  </tfoot>
</table>

.schedule-table thead {
background-color: #f4f4fd;
}

.schedule-table tfoot {
background-color: #e7e9fc;
font-weight: 600;
}

## Важливо

- <thead> — шапка таблиці (заголовки стовпців). Один на таблицю.
- <tbody> — основний вміст. Може бути кілька <tbody> для групування.
- <tfoot> — підвал (підсумки, тотали). Один на таблицю.
- Порядок у коді: thead → tbody → tfoot (браузер відобразить tfoot внизу навіть якщо він у коді перед tbody).
- Розділи дозволяють стилізувати шапку/тіло/підвал окремо та покращують семантику.
- При друку довгих таблиць thead/tfoot повторюються на кожній сторінці.

---

# Заголовок таблиці

Елемент <caption> — заголовок/підпис таблиці. Розміщується одразу після відкриваючого <table>.

<!-- 🆕 caption -->
<table class="schedule-table">
  <caption class="table-caption">Course schedule — Summer 2024</caption>
  <thead>
    <tr>
      <th scope="col">Course</th>
      <th scope="col">Day</th>
      <th scope="col">Time</th>
      <th scope="col">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">HTML</th>
      <td>Mon</td>
      <td>10:00</td>
      <td>2000 UAH</td>
    </tr>
    <tr>
      <th scope="row">CSS</th>
      <td>Wed</td>
      <td>12:00</td>
      <td>2500 UAH</td>
    </tr>
    <tr>
      <th scope="row">JavaScript</th>
      <td>Fri</td>
      <td>14:00</td>
      <td>4000 UAH</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th scope="row">Total</th>
      <td></td>
      <td></td>
      <td>8500 UAH</td>
    </tr>
  </tfoot>
</table>

.table-caption {
margin-bottom: 12px;
font-size: 18px;
font-weight: 600;
text-align: left;
color: #2e2f42;
caption-side: top;
}

Значення caption-side:

- caption-side: top — заголовок зверху (за замовчуванням)
- caption-side: bottom — заголовок знизу таблиці

## Важливо

- <caption> — перший дочірній елемент <table>, перед thead.
- Один <caption> на таблицю.
- Покращує доступність — скрінрідер оголошує caption перед читанням таблиці.
- За замовчуванням центрований — text-align: left для вирівнювання.
- caption-side: bottom — переміщує підпис під таблицю.

---

# Угруповання клітинок

Атрибути colspan та rowspan — об'єднання клітинок по горизонталі та вертикалі.

Базовий принцип:

- colspan="N" — клітинка займає N стовпців (розтягується горизонтально)
- rowspan="N" — клітинка займає N рядків (розтягується вертикально)

## Важливо

- При об'єднанні клітинок потрібно видалити "зайві" <td>/<th> з відповідних рядків.
- colspan="2" — клітинка займає місце двох, тому в цьому рядку на одну <td> менше.
- rowspan="3" — клітинка займає 3 рядки, тому в наступних 2 рядках на одну <td> менше.
- Загальна кількість "колонок" у кожному рядку повинна залишатися однаковою.

---

# Угруповання клітинок: атрибут colspan

Атрибут colspan — об'єднує клітинку по горизонталі (через кілька стовпців).

<!-- 🆕 colspan -->
<table class="schedule-table">
  <caption class="table-caption">Course schedule — Summer 2024</caption>
  <thead>
    <tr>
      <th scope="col">Course</th>
      <th scope="col">Day</th>
      <th scope="col">Time</th>
      <th scope="col">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">HTML</th>
      <td>Mon</td>
      <td>10:00</td>
      <td>2000 UAH</td>
    </tr>
    <tr>
      <th scope="row">CSS</th>
      <td>Wed</td>
      <td>12:00</td>
      <td>2500 UAH</td>
    </tr>
    <tr>
      <th scope="row">JavaScript</th>
      <td>Fri</td>
      <td>14:00</td>
      <td>4000 UAH</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <!-- 🆕 colspan="3" — клітинка займає 3 стовпці -->
      <th colspan="3" scope="row">Total</th>
      <td>8500 UAH</td>
    </tr>
  </tfoot>
</table>

## Важливо

- colspan="3" — клітинка розтягується на 3 стовпці, замінює 3 окремі <td>.
- У рядку з colspan="3" буде на 2 елементи <td>/<th> менше (3 - 1 = 2 видалені).
- Часто використовується у tfoot для підсумкового рядка.
- colspan працює і на <td>, і на <th>.
- Значення colspan не може перевищувати загальну кількість стовпців таблиці.

---

# Угруповання клітинок: атрибут rowspan

Атрибут rowspan — об'єднує клітинку по вертикалі (через кілька рядків).

<!-- 🆕 rowspan -->
<table class="schedule-table">
  <caption class="table-caption">Course schedule — Summer 2024</caption>
  <thead>
    <tr>
      <th scope="col">Day</th>
      <th scope="col">Course</th>
      <th scope="col">Time</th>
      <th scope="col">Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <!-- 🆕 rowspan="2" — клітинка займає 2 рядки -->
      <th rowspan="2" scope="rowgroup">Mon</th>
      <td>HTML</td>
      <td>10:00</td>
      <td>2000 UAH</td>
    </tr>
    <tr>
      <!-- немає <th> для Day — його займає rowspan зверху -->
      <td>CSS</td>
      <td>12:00</td>
      <td>2500 UAH</td>
    </tr>
    <tr>
      <th scope="row">Fri</th>
      <td>JavaScript</td>
      <td>14:00</td>
      <td>4000 UAH</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <th colspan="3" scope="row">Total</th>
      <td>8500 UAH</td>
    </tr>
  </tfoot>
</table>

## Важливо

- rowspan="2" — клітинка розтягується на 2 рядки вниз.
- У наступному рядку (який "поглинається") потрібно видалити відповідну <td>/<th>.
- rowspan + colspan можна комбінувати на одній клітинці.
- scope="rowgroup" — використовується коли <th> з rowspan є заголовком для групи рядків.
- Підрахунок: кожен рядок повинен мати однакову "сумарну ширину" (з урахуванням colspan та rowspan з попередніх рядків).

---

# Висновки

- <table> + <tr> + <td> — базова структура таблиці (контейнер → рядок → клітинка).
- <th> — клітинка-заголовок. scope="col" для стовпця, scope="row" для рядка.
- <thead> / <tbody> / <tfoot> — семантичні розділи таблиці (шапка, тіло, підвал).
- <caption> — заголовок таблиці. Перший елемент після <table>.
- colspan="N" — об'єднання N стовпців горизонтально. Видалити зайві <td> у рядку.
- rowspan="N" — об'єднання N рядків вертикально. Видалити зайві <td> у наступних рядках.
- border-collapse: collapse — обов'язково для прибирання подвійних рамок.