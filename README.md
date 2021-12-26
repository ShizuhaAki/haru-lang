# Harulang

Harulang is a simple scripting language for visual novels.

## Minimum example

```
config
  resource-directory =  "/resources"
end config
character reimu
  name = "Reimu Hakurei"
  img = "/img/reimu"
end character
character marisa
  name = "Marisa Kirisame"
  img = "/img/marisa"
end character
let san = 6
scene main
  show background "/img/hakurei-shrine.jpg"
  show reimu at left
  show marisa at right
  marisa happy "This is a line spoken by Marisa"
  reimu happy "This is a line spoken by Reimu"
  for i = 0 to 10
    aside "This is a for loop, now i = ${i}"
  end for
  select
    choice "Choice 1"
      san = san - 1
    end choice
    choice "Choice 2"
      san = san + 1
      jump scene1_1
    end choice
  end select
  if san < 6 then
    aside "Your san is less than 6"
  end if
end scene
```
