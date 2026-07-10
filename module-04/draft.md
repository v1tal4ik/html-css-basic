# 2D-трансформації

# Масштабування

Властивість transform: scale() — змінює розмір елемента відносно його центру.

Приклад — картка продукту збільшується при hover:

<ul class="products-list">
  <li class="products-item">
    <img class="products-img" src="./images/products/cake.jpg" alt="Cake" width="230" height="201" />
    <h3 class="products-heading">Orange</h3>
    <p class="products-price">45 UAH</p>
  </li>
</ul>

.products-item {
padding: 32px 20px;
border-radius: 15px;
background: #fff;
transition: transform 250ms ease;
}

.products-item:hover {
transform: scale(1.05); /_ 🟢 збільшення на 5% _/
}

Значення scale:

- scale(1) — оригінальний розмір (100%)
- scale(1.5) — збільшення в 1.5 рази (150%)
- scale(0.8) — зменшення до 80%
- scale(2) — збільшення вдвічі
- scale(1.2, 0.8) — ширина ×1.2, висота ×0.8 (деформація)
- scaleX(1.5) — тільки по горизонталі
- scaleY(0.5) — тільки по вертикалі

Приклад — зображення збільшується всередині контейнера:

.products-thumb {
overflow: hidden; /_ 🟢 обрізає те що виходить за межі _/
border-radius: 15px;
}

.products-img {
transition: transform 300ms ease;
}

.products-item:hover .products-img {
transform: scale(1.1); /_ 🟢 zoom-ефект _/
}

## Важливо

- scale() не впливає на сусідів — елемент візуально збільшується але не зміщує потік.
- overflow: hidden на батьку — обрізає збільшене зображення по краях контейнера.
- scale(1.05) — ледь помітне збільшення, елегантний hover. scale(1.2+) — занадто агресивно для карток.
- transform: scale(0) — елемент зникає (розмір = 0). Корисно для анімацій.
- Масштабування відбувається від центру елемента (transform-origin: center за замовчуванням).

---

# Поворот

Властивість transform: rotate() — обертає елемент навколо центру.

Приклад — іконка стрілки обертається при hover:

<a class="hero-link" href="">
  scroll down
  <svg class="hero-link-icon" width="22" height="22">
    <use href="./images/icons.svg#icon-arrow-down"></use>
  </svg>
</a>

.hero-link-icon {
transition: transform 250ms ease;
}

.hero-link:hover .hero-link-icon {
transform: rotate(180deg); /_ 🟢 поворот на 180° _/
}

Значення rotate:

- rotate(0deg) — без повороту
- rotate(45deg) — 45° за годинниковою стрілкою
- rotate(-45deg) — 45° проти годинникової
- rotate(90deg) — чверть оберту
- rotate(180deg) — перевернути
- rotate(360deg) — повний оберт (повертається на місце)

Приклад — декоративний елемент повернутий на 45°:

.decor-square {
width: 40px;
height: 40px;
background: #fd9222;
transform: rotate(45deg); /_ 🟢 ромб _/
}

Зміна центру обертання:

.icon {
transform-origin: center; /_ за замовчуванням _/
}

.icon-corner {
transform-origin: top left; /_ 🟢 обертається навколо лівого верхнього кута _/
}

.icon-bottom {
transform-origin: center bottom; /_ 🟢 обертається навколо нижньої точки _/
}

## Важливо

- rotate() обертає навколо центру елемента (transform-origin: center center).
- transform-origin — змінює точку обертання. Значення: top, bottom, left, right, center, px, %.
- Від'ємні значення — проти годинникової стрілки.
- rotate(360deg) з infinite анімацією — класичний лоадер/спінер.
- Можна комбінувати: transform: rotate(45deg) scale(1.2).

---

# Декоративний оверлей

Властивість transform: translate() — зміщує елемент відносно його початкової позиції.

Приклад — overlay що виїжджає знизу при hover:

<ul class="bestsellers-list">
  <li class="bestsellers-item">
    <div class="bestsellers-thumb">
      <img class="bestsellers-img" src="./images/bestsellers/img-1.jpg" alt="Chocolate" width="368" height="464" />
      <p class="bestsellers-overlay">
        Product made from high-quality dark chocolate with natural cocoa butter.
      </p>
    </div>
    <h3 class="bestsellers-caption">CHOCOLATE WITH NUTS</h3>
  </li>
</ul>

.bestsellers-thumb {
position: relative;
overflow: hidden; /_ 🟢 ховає overlay за межами _/
border-radius: 15px 15px 0 0;
}

.bestsellers-overlay {
position: absolute;
top: 0;
left: 0;
width: 100%;
height: 100%;
padding: 40px;
display: flex;
align-items: center;
color: #fff;
background: linear-gradient(
rgba(253, 146, 34, 0.9),
rgba(253, 146, 34, 0.9)
);
transform: translateY(100%); /_ 🟢 сховано внизу _/
transition: transform 250ms ease; /_ 🟢 _/
}

.bestsellers-item:hover .bestsellers-overlay {
transform: translateY(0); /_ 🟢 виїжджає на місце _/
}

Значення translate:

- translateX(100px) — зміщення вправо на 100px
- translateX(-100px) — зміщення вліво
- translateY(50px) — зміщення вниз
- translateY(-50px) — зміщення вгору
- translate(100px, 50px) — X і Y одночасно
- translateX(100%) — зміщення на 100% ширини самого елемента
- translateY(100%) — зміщення на 100% висоти самого елемента

Варіанти напрямку overlay:

/_ Знизу вгору _/
.overlay { transform: translateY(100%); }
.item:hover .overlay { transform: translateY(0); }

/_ Зверху вниз _/
.overlay { transform: translateY(-100%); }
.item:hover .overlay { transform: translateY(0); }

/_ Зліва _/
.overlay { transform: translateX(-100%); }
.item:hover .overlay { transform: translateX(0); }

/_ Справа _/
.overlay { transform: translateX(100%); }
.item:hover .overlay { transform: translateX(0); }

## Важливо

- translate() не впливає на потік — елемент зміщується візуально, місце зберігається.
- translateY(100%) — це 100% висоти САМОГО елемента, не батька.
- overflow: hidden на батьку — обов'язково щоб overlay було невидимим поза контейнером.
- translate + transition — стандартний паттерн для hover-overlay на картках.
- translate продуктивніший за top/left — не викликає reflow.

---

# Центрування елемента

transform: translate(-50%, -50%) — зміщення на половину власних розмірів. Використовується для центрування абсолютних елементів.

Приклад — модальне вікно по центру екрану:

<div class="backdrop">
  <div class="modal">
    <h2 class="modal-title">Leave a review</h2>
    <form class="modal-form">...</form>
    <button class="modal-close" type="button">×</button>
  </div>
</div>

.backdrop {
position: fixed;
top: 0;
left: 0;
width: 100%;
height: 100%;
background: rgba(0, 0, 0, 0.5);
}

.modal {
position: absolute;
top: 50%; /_ 🟢 50% від верху viewport _/
left: 50%; /_ 🟢 50% від лівого краю _/
transform: translate(-50%, -50%); /_ 🟢 зміщення на половину себе _/
width: 500px;
padding: 40px;
background: #fff;
border-radius: 15px;
}

Як це працює:

- top: 50% — верхній край елемента на середині батька
- left: 50% — лівий край елемента на середині батька
- translate(-50%, -50%) — зміщує елемент назад на половину його власної ширини та висоти
- Результат — центр елемента збігається з центром батька

Інший приклад — кнопка закриття в правому верхньому куті модалки:

.modal-close {
position: absolute;
top: 12px;
right: 12px;
width: 32px;
height: 32px;
display: flex;
align-items: center;
justify-content: center;
background: transparent;
border: none;
cursor: pointer;
}

Центрування без transform (альтернативи):

/_ Flexbox (на батьку) _/
.backdrop {
display: flex;
align-items: center;
justify-content: center;
}

/_ inset + margin auto _/
.modal {
position: absolute;
inset: 0;
margin: auto;
width: 500px;
height: fit-content;
}

## Важливо

- top: 50% + left: 50% + transform: translate(-50%, -50%) — класичне центрування absolute/fixed елементів.
- Працює з будь-яким розміром елемента — не потрібно знати ширину/висоту.
- translate(-50%, -50%) — відсотки рахуються від розміру САМОГО елемента.
- Flexbox на батьку (align-items + justify-content: center) — сучасніша альтернатива.
- Не плутати: top: 50% — це від батька, translate(-50%) — це від самого елемента.

---

# Викривлення

Властивість transform: skew() — нахиляє/перекошує елемент.

Приклад — кнопка з нахиленим фоном:

<button class="btn-skew" type="button">
  <span class="btn-skew-text">Special offer</span>
</button>

.btn-skew {
padding: 14px 40px;
background: #fd9222;
border: none;
border-radius: 4px;
transform: skewX(-12deg); /_ 🟢 нахил контейнера _/
}

.btn-skew-text {
display: inline-block;
transform: skewX(12deg); /_ 🟢 вирівнювання тексту назад _/
}

Значення skew:

- skewX(15deg) — нахил по горизонталі
- skewX(-15deg) — нахил в інший бік
- skewY(10deg) — нахил по вертикалі
- skew(15deg, 5deg) — нахил по X і Y одночасно

Приклад — декоративна смуга під кутом:

.section-decor::before {
content: "";
position: absolute;
top: 0;
left: -5%;
width: 110%;
height: 60px;
background: #fd9222;
transform: skewY(-3deg); /_ 🟢 похила смуга _/
}

## Важливо

- skew() деформує текст всередині — потрібно компенсувати зворотним skew на дочірньому елементі.
- skewX(-12deg) на батьку + skewX(12deg) на тексті — текст рівний, фон похилий.
- Використовується рідко — здебільшого для декоративних елементів та "динамічних" кнопок.
- Великі значення (30deg+) — сильна деформація, виглядає неприродно.
- Можна комбінувати з іншими transform: transform: skewX(-12deg) rotate(2deg).

---

# Комбінування трансформацій

Кілька трансформацій в одному transform — через пробіл:

/_ Збільшити + повернути _/
.card:hover {
transform: scale(1.05) rotate(2deg);
}

/_ Зміститися + збільшити _/
.overlay {
transform: translateY(100%) scale(0.9);
}
.item:hover .overlay {
transform: translateY(0) scale(1);
}

/_ Центрування + масштаб (анімація появи модалки) _/
.modal {
transform: translate(-50%, -50%) scale(0.8);
opacity: 0;
transition: transform 300ms ease, opacity 300ms ease;
}

.modal.is-open {
transform: translate(-50%, -50%) scale(1);
opacity: 1;
}

## Важливо

- Порядок має значення: transform: translateX(100px) rotate(45deg) ≠ transform: rotate(45deg) translateX(100px).
- Трансформації застосовуються справа наліво — остання пишеться, перша виконується.
- Якщо перевизначити transform в :hover — потрібно повторити ВСІ трансформації (translate для центрування + нова).
- transform: none — скасовує всі трансформації.

---

# Висновки

- scale() — масштабування. scale(1.05) для hover-карток, overflow: hidden для обрізки.
- rotate() — обертання. transform-origin змінює точку обертання.
- translate() — зміщення. translateY(100%) + overflow: hidden — overlay-паттерн.
- translate(-50%, -50%) + top/left: 50% — центрування absolute елементів.
- skew() — викривлення. Компенсувати зворотним skew на тексті.
- Комбінування через пробіл. Порядок має значення.
- transform не впливає на потік — елемент візуально змінюється, сусіди не зміщуються.
