# Scroll Detector 

Scroll detector is component to emit event when the component enter client rectangle.

## Demo

[![Edit blue-shadow-t01u6](https://codesandbox.io/static/img/play-codesandbox.svg)](https://codesandbox.io/s/blue-shadow-t01u6?fontsize=14&hidenavigation=1&theme=dark&view=preview)

## Usage

```html
<scroll-detector @enter-client-rect="onEnter">
    <!-- Your content -->
</scroll-detector>
``` 

```javascript
export default {
    methods: {
        onEnter() {
            console.log('detect enter client rect');
        }
    }
}
```

## Events

* into-client-rect
* out-client-rect
* enter-client-rect
* leave-client-rect
* near-client-rect
* far-client-rect

## Properties

* check-when-mounted
* delay-check-when-mounted
* near-range

## Development

Debug

``` 
npm run serve
```

Release 

``` 
npm run build
npm publish
```