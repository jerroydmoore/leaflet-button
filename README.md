leaflet-button
==============

A simple button control for the [Leaflet](http://leafletjs.com) map framework


## Options
The button can be configured with these options
 - **position**: the position of the button. Valid positions are the normal positions for leaflet controls: `topright`,
 `topleft`, `bottomright`, and `bottomleft`.
 - **className**: additional css classes you wish to add to the button.
 - **toggleButton**: Turns the button into a toggle button. The value of toggleButton will be the css Class that is toggled on and off.

## A Simple Example

```javascript
var button = new L.Control.Button('Click me');
button.addTo(map);
button.on('click', function () {
    alert('you clicked the button!');
});
```

## Adding a Toggle button
Setting the option `toggleButton` will turn button into a toggle button. The value you set `toggleButton`
is the css class added to the button, so you can style against it.

In your click handler, you can use the `isToggled()` method to peform conditional actions
```javascript
var button = new L.Control.Button('Toggle me', {
  toggleButton: 'active'
});
button.addTo(map);
button.on('click', function () {
    if (button.isToggled()) {
        sidebar.hide();
    } else {
        sidebar.show();
    }
});
```

## Further Customizing your button
You can use an existing button in your document instead of the default button.
```html
<button id="helpbutton" role="button" class="btn btn-primary">Learn More</button>
```
Create a new button using a reference to the existing button:
```javascript
var button = new L.Control.Button(L.DomUtil.get('helpbutton'), { toggleButton: 'active' });
button.addTo(map);
button.on('click', function () {
    window.location.href = 'http://www.yourdomain.com/help'
});
```

## Example of Integrating it with [L.sidebar](https://github.com/Turbo87/leaflet-sidebar)
```html
<button id="helpbutton" role="button" class="btn btn-primary">Learn More</button>
<div id="helpsidebar">
    <h1>Quick Reference Guide</h1>
    <div>This is the quick help document where you can find useful information about the map you're looking at!
</div>
```
create the sidebar and button in javascript, and link them together using the click handler
```javascript
sidebar = L.control.sidebar('helpsidebar', { position: 'right' });
sidebar.addTo(map);

helpButton = new L.Control.Button(L.DomUtil.get('helpbutton'), { toggleButton: 'active' });
helpButton.addTo(map);
helpButton.on('click', function () {
    if (helpButton.isToggled()) {
        sidebar.hide();
    } else {
        sidebar.show();
    }
});
```
