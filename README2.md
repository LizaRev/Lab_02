# Lab 02

 Проблема `this` у `Ship.fire()`

У JavaScript `this` показує, з яким об'єктом працює метод.

Наприклад:

```js
ship.fire();
```

У цьому випадку `this` всередині `fire()` — це об'єкт `ship`.

Проблема може виникнути, якщо передати метод прямо в обробник клавіатури:

```js
window.addEventListener('keydown', ship.fire);
```

Тоді метод викликається не як `ship.fire()`, тому `this` може бути неправильним.

Це проблема для нашого методу `fire()`, тому що він використовує властивості корабля:

```js
this.world
this.pos
this.vel
this.angle
```

Наприклад, через `this.world` куля додається у світ:

```js
this.world.spawn(bullet);
```

### Виправлення

Один зі способів — викликати метод через об'єкт:

```js
window.addEventListener('keydown', () => {
  ship.fire();
});
```

Також можна використати `bind()`:

```js
window.addEventListener(
  'keydown',
  ship.fire.bind(ship)
);
```

### Як зроблено у моєму проєкті

У моїй  грі клавіатура обробляється через `input.js`.

У `main.js` ми перевіряємо натискання `Space`:

```js
if (input.justPressed('Space')) {
  ship.fire();
}
```

Тобто метод викликається саме через об'єкт `ship`.

Тому всередині `fire()` `this` правильно посилається на корабель.

У результаті `Ship.fire()` може використовувати `this.world`, `this.pos`, `this.vel` і `this.angle` та створювати кулю.



