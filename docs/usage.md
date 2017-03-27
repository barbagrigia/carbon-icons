## Usage

### Using SVG sprite (recommended)

Requirements: 

- Install `@console/bluemix-icons`
- Use `svgxuse` polyfill
	
Full installation details in [GitHub](https://github.ibm.com/Bluemix/bluemix-icons/blob/master/docs/install.md). 

### Using SVG sprite from static assets (recommended)

Use the SVG sprite (__bluemix-icons.svg__) by serving it as a static asset.
Then reference the SVG icon you want to display using a path to the SVG sprite file.
To use SVG sprite files, they __must__ be distributed through a web server and while using `svgxuse`. 

```html
<!-- From static assets  -->
<svg>
  <use xlink:href="/path_to_static-assets/bluemix-icons.svg#icon--icon_name"></use>
</svg>
```

- `path_to_static-assets` is the path to your static assets where `bluemix-icons.svg` is located.
- `icon_name` is the icon name, which will display the corresponding icon. Refer to the [library page](http://design-system.stage1.mybluemix.net/essentials/iconography.html#library) for a full list of icon names

### Using SVG sprite from Bluemix.Common API

__Do not rely on this usage method in production.__

If you want to use the Bluemix.Common files API to use SVG sprite files, then these are your endpoints for the available files:

- current: `https://dev-console.stage1.ng.bluemix.net/api/v5/img/bluemix-icons.svg`
- legacy: `https://dev-console.stage1.ng.bluemix.net/api/v4/img/sprite.svg`


### CSS

You can override size and color with CSS.

```html
<svg class="icon">
  <use xlink:href="/path_to_static-assets/bluemix-icons.svg#icon--icon_name"></use>
</svg>
```

```css
.icon {
  width: 24px;
  height: 24px;
  fill: red;
}
```

All icons in the library are standarized so that they do not include `stroke` or internal spacing (`padding`).

### Inline SVG

If you're unable to use the recommended SVG sprite (bluemix-icons.svg) or `svgxuse`, you can inline SVG directly into your HTML.
Use npm to install bluemix-icons and you'll have access to production-ready SVG files in the [dist](https://github.ibm.com/Bluemix/bluemix-icons/tree/master/dist) folder.

Note that SVG files in dist folder only include most current icons reflected in bluemix-icons.svg and design-system website. 
Files in svg/subfolders are deprecated and should not be used. 

It's still **highly recommended** to use SVG sprite because it will be easier to maintain your production code and keep up with future updates.

### Main files

Bluemix Icons ships with two main SVG files that contain different sets of external SVG sprite files:

| filename | description | supported versions|
|-----|--------|---------------|
|bluemix-icons.svg| Contains current icons (consolidated subset of legacy icons used in Bluemix) | `3.x` and newer|
|bluemix-icons.json| JSON file created from bluemix-icons.svg, used on [design-system-website](http://design-system.stage1.mybluemix.net/essentials/iconography.html#library) | `3.x` and newer|
|bluemix-icons.js| JS module created from bluemix-icons.svg, used in `Icon` React Component in [bluemix-components-react](https://github.ibm.com/Bluemix/bluemix-components-react) | `3.x` and newer|
|sprite.svg| SVG sprite contains legacy icons (deprecated) | `1.x`, `2.x`, `3.x`, `4.x`, `5.x`|
|icons.json| legacy JSON file created from sprite.svg (deprecated) | `1.x`, `2.x`, `3.x`, `4.x`, `5.x`|
|legacy-icons.js| JS module created from sprite.svg | `3.x` only|


### Accessibility (a11y)

For screen reader accessibility, use `<title>` element and `aria-labelledby` attribute.

```html
<svg class="icon" aria-labelledby="uniquie-id">
  <title id="unique-id">Add a new service</title>
  <use xlink:href="/path_to_static-assets/bluemix-icons.svg#icon--add--glyph"></use>
</svg>
```
* The `aria-labelledby` attribute will reference the `id` attribute in the the `<title>` element.
Make sure that you do not duplicate this `id`.
* The `<title>`element will be read by the screen reader to the user so it should describe it's purpose.

### Polyfill Troubleshooting

> __TL;DR:__ It's recommended to install carbon-icons and use SVG sprite files locally because of issues with CORS.

SVG cannot reference an SVG file on a different domain due to CORS (cross-origin scripting security violations).
This means an app running at `localhost:3000` cannot use the sprite on `dev-console.stage1.ng.bluemix...` without the `svgxuse` polyfill library.

The `svgxuse` polyfill adds SVG/use support for IE 9/10/11. 
It also (and more usefully) does a check for if a `<use>` element is missing content (which it would if the request is cross-origin). If the `<use>` element is empty the script requests the SVG file with an old-fashioned `XMLHttpRequest` (this can go cross-origin, assuming the SVG has an appropriate CORS header) and finds the appropriate #hash to populate the `<use>` element.




