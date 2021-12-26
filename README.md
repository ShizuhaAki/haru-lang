# Harulang

Harulang is a set of API to interact with a game written in Haru. The `lang` in
the name is retained for historical purpose, when it was designed to be a full
scripting language.

## Getting Started
First things first: create a Haru object:

```javascript
const haru = new Haru();
```

Before writing your game logic, configure your project first.

```javascript
haru.setConfiguration("resource-dir", "/resources");
// ...
```

Then, define your characters.
```javascript
const r = haru.createCharacter({
  name: "Reimu",
  img: "/img/reimu",
});
// ...
```

You should then register all the scenes you would use in your game.

```javascript
haru.registerScene("main", sceneMain);
```

Finally, write your game logic into the callback:

```javascript
function sceneMain() {
  haru.line(r, "This is line spoken by r");
  const choice = haru.select(["Choice 1", "Choice 2"]);
  if (choice === 0) {
    // The user has chosen choice 1
    sceneSecond();
  } else if (choice === 1) {
    // The user has chosen choice 2
  }
}
```

## API Documentation
### Project Configuration
#### `haru.setConfiguration(key, value)`

Adds key-value pair to the project configuration.

Returns `value`

#### `haru.getConfiguration(key, value)`

Gets key-value pair from the project configuration.

Returns the value associated with key.

### characters

#### `haru.createCharacter(options)`

Creates character with traits set to `options`.

Returns a Character ID that is used to represent this character uniquely throughout
the game.

### Media
All images are represented by a ID unique to the game run. The ID is not "released"
when the image is hidden, thus, it is possible to apply changes to sprites or images
already hidden and restore them later.

If `id` is not allocated yet, a `UndefinedException` will be raised.

#### `haru.showSprite(chr, face, position)`

Shows the sprite `face` of character `chr` at `position`.

Position should be 0, 1, or 2, denoting left, middle and right respectively.

Returns a unique ID denoting the sprite in-game.

#### `haru.showSprite(id, position)`

Shows sprite `id`, used to recover hidden sprites.

#### `haru.moveSprite(id, position)`

Moves the sprite denoted by `id` to `position`

#### `haru.hideSprite(id)`

Removes (hides) the sprite from the game.

Returns nothing.

#### `haru.showBackground(img)`

Shows `img` as the game background.

Raises `FileNotFoundException` if img is not readable.

Returns a unique ID denoting the image.

#### `haru.showBackground(id)`

Shows the image denoted by `id` as background.

If a background is already set, it is kept in place and render priorities are
used to decide which one is shown.

#### `haru.hideBackground(id)`

Hides the background image denoted by `id`.

#### `haru.setRenderPriority(id, pri)`

Sets the render priority of image `id` to `pri`.

Images with higher render priorities are shown in the front. By default, backgrounds
have a priority of `0` and sprites have a priority of `1000000`.

Returns `pri`.

#### `haru.getRenderPriority(id)`

Gets the render priority of image `id`.

Returns `pri`.

#### `haru.addBGM(file)`

Adds BGM `file` to the game.

Returns a unique ID denoting the BGM.

#### `haru.play(id)`

Plays BGM `id`.

#### `haru.pause(id)`

Pauses BGM `id`.

### Game logic

#### `haru.registerScene(name, callback)`

Registers a game scene and associates it with the `callback` function.

Returns nothing.

#### `haru.line(chr, face, content)`

Make character `chr` speak `content`, using sprite `face`.

If `chr = 0`, content is spoken by the aside.

Returns nothing

#### `haru.select(listOfChoices)`

Present a list of choices to the user.

Returns the index of the chosen item
