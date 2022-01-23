---
description: Documentation for Robot operations addon
---

# Robot Operations Addon

This addon allows you to press keys, move the cursor, and perform clicks using Windows and Linux operating system keyboard and mouse.

### See the example below:

1\) Perform a login flow on [example.testproject.io](https://example.testproject.io).

2\) Save the current document as a PDF file.

3\) Take a full-page screenshot using Chrome dev tools.

4\) Navigate to an [upload test](https://ps.uci.edu/\~franklin/doc/file\_upload.html) and upload a file.

5\) Automate HTML5 drag and drop on [W3C](https://www.w3schools.com/html/html5\_draganddrop.asp).

6\) Navigate to [Angular](https://material.angular.io/cdk/drag-drop/examples) and perform drag and drop in all directions.

![Automate any interface using Robot](../../.gitbook/assets/chrome\_jyn0MIUFvq.gif)

### Available Actions

* `Click at coordinates`
* `Drag and drop`
* `Move mouse to coordinates`
* `Press Control+Key`
* `Press Enter`
* `Press Escape`
* `Press multiple key`
* `Press Tab`
* `Print current document`
* `Take full page screenshot`
* `Type text`
* `Upload a file`

Basic actions:

{% tabs %}
{% tab title="Press Enter" %}
Press Enter
{% endtab %}

{% tab title="Press Escape" %}
Press Escape
{% endtab %}

{% tab title="Press Tab" %}
Press Tab
{% endtab %}
{% endtabs %}

These actions take in the following input parameters:

{% tabs %}
{% tab title="Click at coordinates" %}
Accepts **`X`** and **`Y`** coordinates in correlation to screen resolution, for example 1080x1920px screen, accepts `0<=X<=1920, 0<=Y<=1080`).

Accept **`Right`**=true/false, if set to true action will perform right (context) click instead.
{% endtab %}

{% tab title="Move mouse to coordinates" %}
Accepts **`X`** and **`Y`** coordinates in correlation to screen resolution for example 1080x1920px screen, accepts `0<=X<=1920, 0<=Y<=1080`).
{% endtab %}

{% tab title="Drag and drop" %}
Accepts **`X`** and **`Y`** coordinates in correlation to screen resolution, for example 1080x1920px screen, accepts `0<=X<=1920, 0<=Y<=1080`).

Accepts **destination** **`X`** and **`Y`** coordinates.

Accepts **`timeout`** between pixels movement in MS default=1ms.
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Press multiple keys" %}
Accepts up to 3 lowercase characters, letters, or any special key from the following list:

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
{% endtab %}

{% tab title="Press Control+Key" %}
Accepts 1 lowercase character, letter, or a number.
{% endtab %}

{% tab title="Type text" %}
&#x20;Accepts `0-9, a-z, A-Z, _ , ,+,:` and other **lowercase** symbols for example ``[]`-=/.,;``&#x20;
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="Print document" %}
Accepts path to print the document in for example `C:\temp\myFile.pdf`

Accepts **`timeout`** between operations, default=1 second.
{% endtab %}

{% tab title="Upload file " %}
Accepts path to upload a file from local hard disk for example `C:\temp\myFile.pdf`
{% endtab %}

{% tab title="Take full page screenshot (Chromium only)" %}
Takes full page screenshot using multiple key presses on Chromium browsers.

Accepts **`timeout`** between operations, default=1 second.
{% endtab %}
{% endtabs %}

