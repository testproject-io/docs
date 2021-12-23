---
description: Documentation for Robot operations addon
---

# Robot Operations Addon

This addon allows you to press keys, move the cursor, and perform clicks using the operating system keyboard and mouse.

### Available Actions

Basic actions:

* `Press Enter`
* `Press Escape`
* `Press Tab`

These actions take in the following input parameters:

* `Press Control + Key`(accepts 1 lowercase character, letter, or a number)
* `Click at coordinates` (accepts X and Y coordinates in correlation to screen resolution for example 1080x1920px screen, accepts 0<=X<=1920, 0<=Y<=1080)
* `Press multiple keys` (accepts up to 3 lowercase symbols, letters, or any special key from the following list:

| Special keys |
| :----------: |
|     SHIFT    |
|     CTRL     |
|    CONTROL   |
|      ALT     |
|    ESCAPE    |
|      ESC     |
|    COMMAND   |
|    WINDOWS   |
|     START    |
|    WINKEY    |
|   BACKSPACE  |
|      DEL     |
|    DELETE    |
|     HOME     |
|      END     |
|     ENTER    |
|    PAGEUP    |
|   PAGEDOWN   |
|     LEFT     |
|     RIGHT    |
|      UP      |
|     DOWN     |

* `Print document` (accepts path to print the document in for example C:\temp\myFile.pdf)
* `Type text` (accepts `0-9, a-z, A-Z, _ , :` and other **lowercase** symbols for example ``[]`-=/.,;`` )
* `Upload file` (accepts path to upload a file from local hard disk for example C:\temp\myFile.pdf`)`
