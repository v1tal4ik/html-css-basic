# Адаптивна графіка

# Щільність пікселів

Щільність пікселів (DPR — Device Pixel Ratio) — співвідношення фізичних пікселів екрану до CSS-пікселів.

Типові значення DPR:

- DPR 1x — стандартні екрани (старі монітори, бюджетні ноутбуки)
- DPR 2x — Retina дисплеї (MacBook, iPhone, більшість сучасних смартфонів)
- DPR 3x — флагманські смартфони (iPhone Pro Max, Samsung Galaxy S)

Як це впливає на зображення:

- Екран DPR 1x: 1 CSS-піксель = 1 фізичний піксель
- Екран DPR 2x: 1 CSS-піксель = 4 фізичних пікселі (2×2)
- Екран DPR 3x: 1 CSS-піксель = 9 фізичних пікселів (3×3)

Приклад — .card-img з width="300" на різних екранах:

- DPR 1x: потрібне зображення 300×200 px
- DPR 2x: потрібне зображення 600×400 px (щоб було чітким)
- DPR 3x: потрібне зображення 900×600 px

## Важливо

- На Retina-екранах звичайне зображення виглядає розмитим — браузер розтягує пікселі.
- Для чіткості потрібне зображення у 2x або 3x від CSS-розміру відображення.
- DPR можна перевірити: window.devicePixelRatio в консолі або DevTools Device Mode.
- Більшість сучасних пристроїв мають DPR >= 2.
- SVG-зображення не залежать від DPR — вони векторні і завжди чіткі.

---

# CSS-пікселі

CSS-піксель — абстрактна одиниця виміру що не залежить від фізичної щільності екрану.

Приклад — .card-img відображається однаково на різних DPR:

.card-img {
width: 300px; /_ 300 CSS-пікселів _/
height: 200px; /_ 200 CSS-пікселів _/
}

На різних екранах:

- DPR 1x (1920×1080 монітор): 300 CSS-px = 300 фізичних px
- DPR 2x (Retina MacBook 2880×1800): 300 CSS-px = 600 фізичних px
- DPR 3x (iPhone 14, 390×844 CSS-px): 300 CSS-px = 900 фізичних px

Розміри екранів у CSS-пікселях (viewport):

- iPhone 14: 390×844 CSS-px (фізичних 1170×2532, DPR 3x)
- iPad: 768×1024 CSS-px (фізичних 1536×2048, DPR 2x)
- MacBook Pro 14": 1512×982 CSS-px (фізичних 3024×1964, DPR 2x)

## Важливо

- Media queries працюють з CSS-пікселями, не з фізичними.
- width/height в HTML та CSS — це CSS-пікселі.
- iPhone з шириною 1170 фізичних px має viewport 390 CSS-px (1170 / 3 = 390).
- Тому @media (min-width: 768px) спрацює на iPad (768 CSS-px), але не на iPhone (390 CSS-px).
- Атрибути width="300" height="200" у .card-img — це CSS-пікселі.

---

# Растрові зображення

Растрові зображення (JPEG, PNG, WebP) — складаються з пікселів і мають фіксовану роздільну здатність.

Формати та їх використання для зображень базової розмітки:

- JPEG — .about-img, .card-img (фотографії, складні зображення з градієнтами)
- PNG — .logo якщо потрібна прозорість (іконки, логотипи з прозорим фоном)
- WebP — сучасна альтернатива JPEG/PNG (менший розмір, підтримує прозорість)
- AVIF — найновіший формат (ще менший розмір, обмежена підтримка)

Проблема растрових зображень на Retina:

- .card-img src="images/design.jpg" (300×200 px)
- На DPR 2x екрані відображається в області 600×400 фізичних пікселів
- Браузер розтягує 300×200 до 600×400 — зображення розмите

Рішення — підготувати зображення у кількох розмірах:

- images/design.jpg — 300×200 (для DPR 1x)
- images/design@2x.jpg — 600×400 (для DPR 2x)
- images/design@3x.jpg — 900×600 (для DPR 3x)

## Важливо

- Растрове зображення чітке тільки коли його реальний розмір >= розмір відображення × DPR.
- Більше зображення = більший розмір файлу = повільніше завантаження.
- Потрібен баланс: не відправляти 3x зображення на 1x екран.
- WebP на 25-35% менший за JPEG при однаковій якості — рекомендований формат.
- SVG для іконок та логотипів — не потребує ретинізації.

---

# Ретинізація графіки

Ретинізація — підготовка та відображення зображень підвищеної роздільної здатності для Retina-екранів.

Спосіб 1 — srcset з дескриптором щільності (для .card-img):

<img
  class="card-img"
  src="images/design.jpg"
  srcset="images/design.jpg 1x, images/design@2x.jpg 2x"
  alt="Design"
  width="300"
  height="200"
/>

Спосіб 2 — srcset з дескриптором ширини + sizes:

<img
  class="card-img"
  src="images/design.jpg"
  srcset="images/design-300.jpg 300w, images/design-600.jpg 600w, images/design-900.jpg 900w"
  sizes="(min-width: 1200px) 300px, (min-width: 768px) 50vw, 100vw"
  alt="Design"
  width="300"
  height="200"
/>

Спосіб 3 — елемент <picture> (для .about-img):

<picture>
  <source
    srcset="images/about.webp 1x, images/about@2x.webp 2x"
    type="image/webp"
  />
  <source
    srcset="images/about.jpg 1x, images/about@2x.jpg 2x"
    type="image/jpeg"
  />
  <img class="about-img" src="images/about.jpg" alt="Our team" width="600" height="400" />
</picture>

## Важливо

- srcset з 1x/2x — найпростіший спосіб ретинізації. Браузер сам обирає потрібне зображення.
- srcset з w-дескриптором — гнучкіший, враховує і DPR і розмір viewport.
- sizes — підказка браузеру який розмір зображення буде на екрані (для вибору з srcset).
- <picture> — дозволяє вказати різні формати (WebP з fallback на JPEG).
- src — fallback для старих браузерів що не підтримують srcset.
- Браузер завантажує ТІЛЬКИ одне зображення з srcset — не всі.

---

# Гумові зображення

Гумові (fluid) зображення — масштабуються разом з контейнером, не виходячи за його межі.

Приклад — .card-img та .about-img як гумові зображення:

/_ Базове правило для всіх зображень _/
img {
display: block;
max-width: 100%;
height: auto;
}

/_ .about-img займає всю ширину контейнера _/
.about-img {
width: 100%;
height: auto;
}

/_ .card-img займає всю ширину картки _/
.card-img {
width: 100%;
height: auto;
}

Як працює max-width: 100%:

- Зображення ніколи не буде ширшим за батьківський контейнер
- Якщо контейнер вужчий за зображення — зображення зменшується
- Якщо контейнер ширший за зображення — зображення залишається свого розміру
- height: auto — зберігає пропорції при масштабуванні

Різниця між width: 100% та max-width: 100%:

- width: 100% — зображення ЗАВЖДИ займає 100% ширини контейнера (розтягується)
- max-width: 100% — зображення не перевищує контейнер, але не розтягується більше свого розміру

## Важливо

- max-width: 100%; height: auto — обов'язкове правило для респонсивних зображень.
- display: block — прибирає зайвий відступ знизу (inline-елемент має baseline gap).
- Атрибути width/height в HTML потрібні для резервування місця (запобігає layout shift).
- Без height: auto зображення деформується при зміні ширини.
- object-fit: cover — якщо потрібно обрізати зображення зберігаючи пропорції.

---

# Респонсивні зображення

Респонсивні зображення — різні зображення для різних розмірів viewport (не тільки DPR, а й розмір).

Приклад — .about-img різного розміру на різних breakpoints:

<picture>
  <source
    media="(min-width: 1200px)"
    srcset="images/about-desktop.jpg 1x, images/about-desktop@2x.jpg 2x"
  />
  <source
    media="(min-width: 768px)"
    srcset="images/about-tablet.jpg 1x, images/about-tablet@2x.jpg 2x"
  />
  <img
    class="about-img"
    src="images/about-mobile.jpg"
    srcset="images/about-mobile.jpg 1x, images/about-mobile@2x.jpg 2x"
    alt="Our team"
    width="600"
    height="400"
  />
</picture>

Приклад — .card-img з sizes для автоматичного вибору:

<img
  class="card-img"
  src="images/design-300.jpg"
  srcset="images/design-300.jpg 300w, images/design-600.jpg 600w, images/design-900.jpg 900w"
  sizes="(min-width: 1200px) 340px, (min-width: 768px) 336px, calc(100vw - 32px)"
  alt="Design"
  width="300"
  height="200"
/>

Як браузер обирає зображення (sizes + srcset з w):

- Визначає viewport (наприклад 375px — мобільний)
- Знаходить відповідний sizes: calc(100vw - 32px) = 343px
- Множить на DPR: 343 × 2 = 686px (для Retina)
- Обирає найближче з srcset: 900w (images/design-900.jpg)

## Важливо

- <picture> з media — різні кадрування/пропорції для різних екранів (art direction).
- srcset з w + sizes — один і той же кадр, але різний розмір файлу.
- sizes обов'язковий при використанні w-дескриптора в srcset.
- Браузер сам вирішує яке зображення завантажити — sizes лише підказка.
- На мобільному не потрібне зображення 1200px шириною — економія трафіку.
- Завжди вказувати width/height для запобігання CLS (Cumulative Layout Shift).

---

# Фонові зображення

Фонові зображення — встановлюються через CSS і потребують окремого підходу до ретинізації.

Приклад — .hero з фоновим зображенням (Mobile First):

/_ Mobile — фон 1x _/
.hero {
background-image: url("../images/hero-mobile.jpg");
background-repeat: no-repeat;
background-position: center;
background-size: cover;
padding: 120px 0;
}

/_ Mobile — Retina 2x _/
@media (min-resolution: 192dpi) {
.hero {
background-image: url("../images/hero-mobile@2x.jpg");
}
}

/_ Tablet — фон 1x _/
@media (min-width: 768px) {
.hero {
background-image: url("../images/hero-tablet.jpg");
}
}

/_ Tablet — Retina 2x _/
@media (min-width: 768px) and (min-resolution: 192dpi) {
.hero {
background-image: url("../images/hero-tablet@2x.jpg");
}
}

/_ Desktop — фон 1x _/
@media (min-width: 1200px) {
.hero {
background-image: url("../images/hero-desktop.jpg");
}
}

/_ Desktop — Retina 2x _/
@media (min-width: 1200px) and (min-resolution: 192dpi) {
.hero {
background-image: url("../images/hero-desktop@2x.jpg");
}
}

Медіа-функції для DPR:

- min-resolution: 192dpi — DPR >= 2 (192 / 96 = 2)
- min-resolution: 288dpi — DPR >= 3
- min-device-pixel-ratio: 2 — застарілий варіант (webkit)

Підтримка WebP у фонових зображеннях:

/_ WebP з fallback _/
.hero {
background-image: url("../images/hero-mobile.jpg");
}

.webp .hero {
background-image: url("../images/hero-mobile.webp");
}

@media (min-resolution: 192dpi) {
.hero {
background-image: url("../images/hero-mobile@2x.jpg");
}

.webp .hero {
background-image: url("../images/hero-mobile@2x.webp");
}
}

## Важливо

- background-size: cover — зображення покриває весь елемент зберігаючи пропорції.
- min-resolution: 192dpi — стандартний спосіб перевірки Retina у медіазапитах.
- Для фонових зображень немає srcset — тільки медіазапити.
- Кожна комбінація breakpoint + DPR = окремий медіазапит (може бути 6+ правил).
- Порядок: спочатку breakpoint, потім DPR всередині цього breakpoint.
- background-image не завантажується якщо елемент прихований (display: none) — оптимізація.

---

# Висновки

- DPR — співвідношення фізичних пікселів до CSS-пікселів (1x, 2x, 3x).
- CSS-пікселі — абстрактна одиниця, media queries працюють з ними.
- Растрові зображення потребують версій для різних DPR (300px → 600px для 2x).
- Ретинізація: srcset з 1x/2x, srcset з w + sizes, або <picture>.
- Гумові зображення: max-width: 100%; height: auto — базове правило.
- Респонсивні зображення: різні файли для різних viewport через <picture> або sizes.
- Фонові зображення: медіазапити з min-resolution: 192dpi для Retina.
