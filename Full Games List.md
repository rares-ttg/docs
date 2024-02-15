

## Game Collections

```dataview
LIST
FROM #game-collection 
SORT file.name ASC
```

## Slots
```dataview
LIST 
FROM #game/slots 
SORT file.name ASC
```

## Card Games
```dataview
LIST
FROM #game/cards 
SORT file.name ASC
```
## Roulette
```dataview
LIST
FROM #game/roulette 
SORT file.name ASC
```
## Lotto
```dataview
LIST 
FROM #game/lotto 
SORT file.name ASC
```
## Dice Games
```dataview
LIST
FROM #game/dice  
SORT file.name ASC
```
## Other

```dataview
LIST
FROM #game AND -#game/dice AND -#game/cards AND -#game/slots  AND -#game/lotto AND -#game/roulette
```