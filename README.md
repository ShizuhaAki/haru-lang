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

### API Documentation
#### Project Configuration
##### `haru.setConfiguration(key, value)`

Adds key-value pair to the project configuration.

Returns `value`

##### `haru.getConfiguration(key, value)`

Gets key-value pair from the project configuration.

Returns the value associated with key.

#### characters

##### `haru.createCharacter(options)`

Creates character with traits set to `options`.

Returns a Character ID that is used to represent this character uniquely throughout
the game.

#### Game logic

##### `haru.registerScene(name, callback)`

Registers a game scene and associates it with the `callback` function.

Returns nothing.

##### `haru.line(chr, content)`

Make character `chr` speak `content`, if `chr = 0`, content is spoken by the aside.

Returns nothing

##### `haru.select(listOfChoices)`

Present a list of choices to the user.

Returns the index of the chosen item
