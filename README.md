
# Google Sites Anit-Pointer Lock Bypass - V1.2

Ok, it's not the best title but it works. Let me know of a better one please.  

To explain this simply, this is a way to bypass the way Google Sites blocks you from locking your cursor/pointer/mouse in embeds. It was originally made by the user [binary-person](https://github.com/binary-person). However, it wasn't posted on GitHub and it was a little odd-looking if you could extract it. So, I figured I could spruce it up a bit and possibly improve its usability.

## Features

- Bypassing the anti-cursor locking on google sites
- Does not add opened site to browsing history.*
- Web filters do not detect traffic of the site.**
- Sites have a lower risk getting blocked when there is a web filter.

## How can I use it?

There are four files to choose from and they all have the same basic functions.

- [`index.html`](/index.html) It is the main one that is updated the most but it's as efficient as `insert.html`. It also doesn't look very good.
- [`insert.html`](/insert.html) This is the optimized version that I recommend using for your projects. It is optimized to run slightly faster and looks a lot smaller in comparison.
- [`customLaunch.html`](/customLaunch.html) This file is to be saved locally and used to choose what website you want to go to.
- [`multi-button.html`](/multi-button.html) This is a testing file to support multiple buttons in a single embed. It is in very early development

No matter which one you choose, at the beginning it will have two variables you can change. However, `customLaunch.html` will look slightly different.

```js
var url = "https://mywebsite.com";
var appName = "MyApp";
```

These two variables are the website URL you want it to open and the name of what app you are using. This is used when the program displays: `Press Button to Launch [Your App Name]`

## How Does It Work?

**Opening**  
When you press the button it opens a new window, formats the body properly. To do it it sets the margin to 0 and the viewport height (vh) to 100 which is read as a percentage. Finally, it adds an iFrame element into the window.

```js
win = window.open(); //open the window
win.document.body.style.margin = "0"; //set margin to 0
win.document.body.style.height = "100vh"; //make sure the viewport is as tall as possible
var  iframe = win.document.createElement("iframe"); //add iframe element
```

Next, it will configure the iframe. This is done by removing the border, setting the width and height to 100%, and making the margins around the iframe 0. Lastly, it adds the target URL as an `src`. That's it!

```js
iframe.style.border = "none"; // removing border
iframe.style.width = "100%"; // make iframe as wide as possible 
iframe.style.height = "100%"; // make iframe as tall as possible
iframe.style.margin = "0"; // removing margin
iframe.src = url; //the url variable is stored at the begnning for convenience
```

**Switching Back To Open Tab**  
Now the whole thing could've been left back at just opening but it's not very convenient.  In this case, we have it focus the user to the window when the button is clicked.

```js
if (win) { // if win has value, then it proceeeds to run the code
  win.focus();
} 
else {
win = window.open()
//continues into window opening
```

Finally, at the end of the else statement, we add a line of code to tell the user to click the button to switch back. (This is shown before the user focuses the window)

```js
titleText.textContent = appName + " is running. Click the button to switch to that tab.";
```

**Reopening the Tab**  
To reopen the tab it constantly runs a function every 500 milliseconds (or half a second). This function states if the window (the variable `win`) is closed then it will clear the interval used to run the function. Next, it will clear the data from the variable `win` and display an updated message to the user to click the button to reopen the tab.

```js
var  interval = setInterval(function() {
    if (win.closed) {
    clearInterval(interval);
    win = undefined;
    titleText.textContent = appName + " closed. Click button to reopen the game";
  }
}, 500);
```

**The Rest of It**  
The rest of it is small technical things like stylesheets and storage of the app name etc.

---

> Credits:  
> [Reed Graf](https://github.com/ReedGraf) - Main HTML front, some JavaScript manipulation  
> [Bianary Person](https://github.com/binary-person) - Original Code  

> Contact Info:  
> Email: [isd279Games@gmail.com](mailto:isd279Games@gmail.com)

###### * = Tested on chrome
###### ** = Tested on Lightspeed Filter
