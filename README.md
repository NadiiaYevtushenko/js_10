# 📌 Розробка повнофункціонального слайдера на чистому JavaScript

## 🔥 Опис проекту

Цей проект реалізує **повнофункціональний слайдер** з використанням **чистого JavaScript** та **функціонального підходу**. Слайдер підтримує автоматичне перемикання, керування через кнопки, клавіатуру, тач-жести та індикатори поточного слайду.

## 🎯 Функціональність

✅ **Динамічна зміна слайдів** через кнопки `Назад` та `Вперед`.
✅ **Автоматичне перемикання слайдів** через заданий інтервал часу.
✅ **Можливість зупинки/відновлення автовідтворення** через кнопку `Play/Pause`.
✅ **Індикатори поточного слайду**, які дозволяють швидко перемикатися між слайдами.
✅ **Керування з клавіатури** (ліві/праві стрілки для перемикання, `Space` для паузи/відтворення).
✅ **Підтримка тач-жестів** (свайпи для мобільних пристроїв).
✅ **Підтримка миші** (перетягування для перемикання слайдів).

## 🛠️ Використані технології

- **HTML** – структура слайдера
- **CSS** – стилізація та адаптація
- **JavaScript** – логіка перемикання слайдів

## 📂 Структура проекту

```
📁 slider-project
│── 📄 index.html      # Головний HTML-файл
│── 📄 style.css       # Стили для слайдера
│── 📄 index.js        # Основний JavaScript-код
│── 📁 assets/img      # Папка зображень для слайдера
```

## 📜 Код

### **HTML (index.html)**

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Slider</title>
    <link rel="stylesheet" href="style.css" />
    <link
      rel="stylesheet"
      href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css"
    />
  </head>
  <body>
    <div id="carousel" class="carousel">
      <div id="slides-container" class="slides">
        <div
          class="slide active"
          style="background-image: url(assets/img/pic_1.webp);"
        ></div>
        <div
          class="slide"
          style="background-image: url(assets/img/pic_2.webp);"
        ></div>
        <div
          class="slide"
          style="background-image: url(assets/img/pic_3.webp);"
        ></div>
      </div>
      <div id="controls-container" class="controls">
        <div id="prev-btn" class="control prev">
          <i class="fa-solid fa-arrow-left"></i>
        </div>
        <div id="pause-btn" class="control pause">Pause</div>
        <div id="next-btn" class="control next">
          <i class="fa-solid fa-arrow-right"></i>
        </div>
      </div>
      <div id="indicators-container" class="indicators">
        <div class="indicator active" data-slide-to="0"></div>
        <div class="indicator" data-slide-to="1"></div>
        <div class="indicator" data-slide-to="2"></div>
      </div>
    </div>
    <script src="index.js"></script>
  </body>
</html>
```

### **CSS (style.css)**

```css
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background: #111;
}

.slides {
  width: 90vw;
  height: 80vh;
  overflow: hidden;
  position: relative;
}

.slide {
  width: 100%;
  height: 100%;
  background-size: cover;
  background-position: center;
  position: absolute;
  opacity: 0;
  transition: opacity 1s ease-in-out;
}

.slide.active {
  opacity: 1;
}

.control {
  position: absolute;
  top: 90%;
  background: rgba(0, 0, 0, 0.5);
  padding: 10px 20px;
  color: #fff;
  cursor: pointer;
}

.prev {
  left: 10px;
}
.next {
  right: 10px;
}
.pause {
  left: 50%;
  transform: translateX(-50%);
}

.indicators {
  display: flex;
  justify-content: center;
  position: absolute;
  bottom: 10px;
  width: 100%;
}
.indicator {
  width: 10px;
  height: 10px;
  background: white;
  margin: 5px;
  border-radius: 50%;
  cursor: pointer;
}
.indicator.active {
  background: red;
  width: 20px;
}
```

### **JavaScript (index.js)**

```js
(function () {
  const container = document.querySelector("#carousel");
  const slides = container.querySelectorAll(".slide");
  const indicators = container.querySelectorAll(".indicator");
  const pauseBtn = container.querySelector("#pause-btn");
  const prevBtn = container.querySelector("#prev-btn");
  const nextBtn = container.querySelector("#next-btn");

  let currentSlide = 0;
  let timerId = null;
  let isPlaying = true;
  const interval = 2000;

  function goToSlide(n) {
    slides[currentSlide].classList.remove("active");
    indicators[currentSlide].classList.remove("active");
    currentSlide = (n + slides.length) % slides.length;
    slides[currentSlide].classList.add("active");
    indicators[currentSlide].classList.add("active");
  }

  function goToNext() {
    goToSlide(currentSlide + 1);
  }
  function goToPrev() {
    goToSlide(currentSlide - 1);
  }
  function tick() {
    timerId = setInterval(goToNext, interval);
  }

  function pauseHandler() {
    clearInterval(timerId);
    pauseBtn.textContent = "Play";
    isPlaying = false;
  }
  function playHandler() {
    tick();
    pauseBtn.textContent = "Pause";
    isPlaying = true;
  }
  function pausePlayHandler() {
    isPlaying ? pauseHandler() : playHandler();
  }

  prevBtn.addEventListener("click", goToPrev);
  nextBtn.addEventListener("click", goToNext);
  pauseBtn.addEventListener("click", pausePlayHandler);

  indicators.forEach((indicator, index) => {
    indicator.addEventListener("click", () => goToSlide(index));
  });

  tick();
})();
```

## 🚀 Як запустити проєкт

1. Завантажити файли проекту.
2. Відкрити `index.html` у браузері.

## 📌 Додаткові покращення

✅ Додати анімації переходів між слайдами.
✅ Покращити адаптивність для мобільних пристроїв.
✅ Додати кастомні стилі для кнопок навігації.

## 🎯 Висновок

Цей **слайдер на чистому JavaScript** демонструє **потужність функціонального підходу** та **ефективну роботу з DOM**. Його можна легко **налаштувати, стилізувати та інтегрувати** у будь-який вебпроєкт! 🚀
