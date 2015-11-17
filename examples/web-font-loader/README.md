# Web Font Loader example

The [Web Font Loader](https://github.com/typekit/webfontloader) gives developers added control when using linked fonts via `@font-face`. We can use the Flash of Unstyled Text to give users immediate access to the content and then add classes to the document to show the new fonts once they’ve been loaded.

This method is co-developed by Google and Typekit.


## Walkthrough

### 1. Add the Web Font Loader script to the page.

In this instance we’re using the `async` attribute on the script so that it doesn’t block loading.

```html
<script src="https://ajax.googleapis.com/ajax/libs/webfont/1.5.18/webfont.js" async></script>
```



### 2. Make the preconnect handshake to the font vendor of your choice.

This code can be added the `head` of the document. [Read more about preloading assets.](https://css-tricks.com/prefetching-preloading-prebrowsing/)

```html
<link rel="preconnect" href="https://fonts.typonine.com/" crossorigin>
```



### 3. Add settings to the `WebFontConfig` object.

The `timeout` is entirely optional but makes sure that we’re not wasting the users time trying to download assets on a slow network.

The `active` function here is entirely optional, however it gives us the option to set `sessionStorage` data.

```js
WebFontConfig = {
  custom: {
    families: [
      'Nocturno Display Medium 3',
      'Nocturno Book 2',
      'Nocturno Regular Italic 24',
      'Nocturno Regular 26',
      'Nocturno Regular 25'
    ],
    urls: [
      'https://fonts.typonine.com/WF-000000-001254.css',
      'https://fonts.typonine.com/WF-000000-001255.css'
    ]
  },
  timeout: 2000,
  active: function() {
    sessionStorage.fonts = true;
  }
};
```




### 4. Check if fonts have already been cached.

With the `active` event we set up we can now check in the `head` of the document if our fonts are already cached and change the classname just a little bit faster:

```html
<head>
  <script>
    (function() {
      if (sessionStorage.fonts) {
        console.log("Fonts installed.");
        document.documentElement.classList.add('wf-active');
      } else {
        console.log("No fonts installed.");
      }
    })();
  </script>
</head>
```



## Support

This technique supports fonts from Google Fonts, Typekit, Fonts.com, and Fontdeck, as well as self-hosted web fonts.


## Documentation and tutorials

- [Official docs](https://github.com/typekit/webfontloader)
- [CSS-Tricks tutorial on the Web Font Loader](https://css-tricks.com/loading-web-fonts-with-the-web-font-loader/)



