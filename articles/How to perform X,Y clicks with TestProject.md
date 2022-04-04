---
description: >-
  Click or Tap at Coordinates - X/Y clicks on Web, and tap at coordinates for
  Mobile
---

# How to perform X,Y clicks with TestProject

### **How to perform X,Y click with TestProject?** <a href="#h_6bd81c6d03" id="h_6bd81c6d03"></a>

To perform X, Y click on Web with TestProject, we will first need to find the coordinates (x,y) of the page. to do so we will open the session dev tools using right-click -> inspect or F12 on the keyboard.

![](https://downloads.intercomcdn.com/i/o/340548899/8480d1f312721691a070c1c1/image.png)

After we opened the dev tools we will navigate to the "Console" tab, and type this command to find our current mouse position:

```javascript
document.onmousemove = function(e){
var x = e.clientX;
var y = e.clientY;
var a = e.clientX;
var b = e.clientY;
document.title = "X is "+x+" and Y is "+y;
e.target.title = "X is "+a+" and Y is "+b;
};
```

it should look like this:

![](https://downloads.intercomcdn.com/i/o/340549426/fec4ba9c1fdb43177de229c0/image.png)

We can either use the new tab name or the tooltip we have added.

After we retrieved the X, Y coordinates, we will execute a step from the addon Web Extensions named Execute JavaScript.

![](https://downloads.intercomcdn.com/i/o/340549855/e699ec1c8ae5aca0aec0317f/image.png)

We will type this into our Code input to click on the exact coordinates:

```javascript
document.elementFromPoint(x,y).click();
```

Don't forget to replace (x, y) with the coordinates.

If you followed all these instructions it should look like this:

![](https://downloads.intercomcdn.com/i/o/340550861/52822a6d51401f340174da67/image.png)

### **For Mobile tap at X, Y coordinates:** <a href="#h_6688e64dea" id="h_6688e64dea"></a>

To tap anywhere on the mobile screen at coordinates we will use the step " tap gesture at coordinates".

![](https://downloads.intercomcdn.com/i/o/340551521/78fb81cdb65965384fe559d4/image.png)

To find the X, Y we will use the TestProject recorder.

We can locate the coordinates on the top right corner of the screen.

Then we will set them in the inputs fields of the step.

It should look like this:

\


![](https://downloads.intercomcdn.com/i/o/340552459/09af86b4ccdff90d285bbc25/image.png)
