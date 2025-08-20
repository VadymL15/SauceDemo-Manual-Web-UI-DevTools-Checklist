# E2E Сценарій: SauceDemo (Манульне тестування + Chrome DevTools)

**Мета:** Перевірити повний позитивний сценарій: Вхід → Додавання в кошик → Оформлення замовлення → Завершення → Вихід, з використанням DevTools (Network, Application, Console, Timing).

**Середовище та дані**
- Сайт: https://www.saucedemo.com/
- Користувач: `standard_user` / `secret_sauce`
- Браузер: Chrome (DevTools)

---

## 0) Підготовка
1. Відкрити DevTools (F12 / Ctrl+Shift+I).
2. **Network**: включити **Disable cache** + **Preserve log**, обрати фільтр **XHR/Fetch**.
3. (Опційно) **Throttling**: спочатку **No throttling**, потім перевірити **Slow 3G**.
4. Очистити **Application → Local/Session Storage** та **Cookies**.

**Артефакти**
- Скриншот: DevTools з налаштованою вкладкою Network.

---

## 1) Логін
**Кроки**
1. Перейти на `https://www.saucedemo.com/`.
2. Ввести `standard_user / secret_sauce`.
3. Натиснути **Login**.

**Очікування (UI)**
- Перенаправлення на сторінку **Products**.
- Видимий заголовок “Products”.

**DevTools перевірки**
- **Network**: перевірити запити (200/302, заголовки, відповіді, час).
- **Console**: немає JS-помилок.
- **Application**: перевірити Local/Session Storage і Cookies.

**Артефакти**
- HAR: `har/login-success.har`
- Скриншот: `products-after-login.png`
- Скриншот: `storage-after-login.png`

**Критерії прийняття**
- Немає 4xx/5xx.
- Дані сесії збережені у сховищі.

---

## 2) Додавання товару в кошик
**Кроки**
1. На сторінці **Products** натиснути **Add to cart**.
2. Бейдж кошика = 1, кнопка = **Remove**.
3. Перезавантажити сторінку.

**Очікування (UI)**
- Бейдж кошика = 1.
- Стан кнопки збережено.

**DevTools перевірки**
- **Network**: XHR → статус 200, правильний payload.
- **Application**: стан кошика збережений.

**Артефакти**
- HAR: `har/add-to-cart.har`
- Скриншот: `cart-badge-1.png`

**Критерії прийняття**
- Стан кошика збережений після reload.

---

## 3) Деталі продукту
**Кроки**
1. Відкрити товар → **Product Details**.
2. Натиснути **Back**.

**Очікування**
- Деталі відображаються.
- Повернення зберігає стан (кошик, сортування).

**DevTools**
- **Network**: немає 404, всі ресурси завантажені.

**Артефакти**
- Скриншот: `product-details.png`.

---

## 4) Кошик → Checkout (інформація користувача)
**Кроки**
1. Перейти в кошик.
2. Натиснути **Checkout**.
3. Спробувати продовжити з пустими полями (негатив).
4. Заповнити форму та продовжити.

**Очікування**
- Негатив: помилка біля пустих полів.
- Позитив: перехід до **Overview**.

**DevTools**
- **Network**: запити при Continue → 200.
- **Console**: немає помилок.

**Артефакти**
- Скриншот: `checkout-info-error.png`
- Скриншот: `checkout-info-filled.png`

---

## 5) Checkout → Завершення
**Кроки**
1. На Overview перевірити товари, totals, tax.
2. Натиснути **Finish**.

**Очікування**
- Сторінка **Checkout: Complete!** з повідомленням.
- Кошик очищений.

**DevTools**
- **Network**: всі запити 200.
- **Timing**: час відповіді в нормі.

**Артефакти**
- HAR: `har/checkout-complete.har`
- Скриншот: `checkout-complete.png`

---

## 6) Вихід
**Кроки**
1. Відкрити меню → **Logout**.

**Очікування**
- Повернення на сторінку Login.

**DevTools**
- **Application**: Storage і Cookies очищені.
- **Network**: перевірити запит logout.

**Артефакти**
- HAR: `har/logout.har`
- Скриншот: `login-after-logout.png`

---

## 7) (Опційно) Повільна мережа / Offline
**Slow 3G**
- Очікування: індикатори завантаження, без зависань.

**Offline**
- Очікування: адекватні помилки, без крешів.

**Артефакти**
- Скриншот: `timing-slow3g.png`
- Скриншот: `offline-add-to-cart.png`

---

## 8) Accessibility
**Кроки**
1. Перевірити навігацію через Tab/Shift+Tab.
2. Зображення мають alt.
3. Запустити Lighthouse (Accessibility).

**Артефакти**
- Lighthouse HTML: `lighthouse-accessibility.html`
- Скриншот: `a11y-tab-focus.png`.

---

## Структура артефактів
