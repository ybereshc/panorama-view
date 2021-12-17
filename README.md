- [Class: **EventDispatcher**][EventDispatcher]
	- [dispatcher.addEventListener( _type, callback_ )](#dispatcheraddeventlistener-type-callback-)
	- [dispatcher.removeEventListener( _type, callback_ )](#dispatcherremoveeventlistener-type-callback-)
	- [dispatcher.hasEventListener( _type, callback_ )](#dispatcherhaseventlistener-type-callback-)
	- [dispatcher.dispatchEvent( _event_ )](#dispatcherdispatchevent-event-)
- [Class: **Controls**][Controls]
	- [**static** Controls.default](#static-controlsdefault)
	- [controls.rotateMouseButton](#controlsrotatemousebutton)
	- [controls.rotateTouchCount](#controlsrotatetouchcount)
	- [controls.keys](#controlskeys)
	- [controls.azimuthAngle](#controlsazimuthangle)
	- [controls.minAzimuthAngle](#controlsminazimuthangle)
	- [controls.maxAzimuthAngle](#controlsmaxazimuthangle)
	- [controls.polarAngle](#controlspolarangle)
	- [controls.minPolarAngle](#controlsminpolarangle)
	- [controls.maxPolarAngle](#controlsmaxpolarangle)
	- [controls.fov](#controlsfov)
	- [controls.minFov](#controlsminfov)
	- [controls.maxFov](#controlsmaxfov)
	- [controls.autoRotate](#controlsautorotate)
	- [controls.enabled](#controlsenabled)
	- [controls.zoomEnabled](#controlszoomenabled)
	- [controls.rotateEnabled](#controlsrotateenabled)
	- [controls.wheelEnabled](#controlswheelenabled)
	- [controls.pointerEnabled](#controlspointerenabled)
	- [controls.keyboardEnabled](#controlskeyboardenabled)
	- [controls.dispose()](#controlsdispose)
	- [controls.setZoom( _val, force_ )](#controlssetzoom-val-force-)
	- [controls.zoom( _val, force_ )](#controlszoom-val-force-)
	- [controls.setRotate( _theta, phi, force_ )](#controlssetrotate-theta-phi-force-)
	- [controls.rotate( _theta, phi, force_ )](#controlsrotate-theta-phi-force-)
	- [controls.reset()](#controlsreset)
- [Class: **Raycasts**][Raycasts]
	- [raycasts.one](#raycastsone)
	- [raycasts.enabled](#raycastsenabled)
	- [raycasts.dispose()](#raycastsdispose)
	- [raycasts.getIntersects( _pos_ )](#raycastsgetintersects-pos-)
- [Class: **Panorama**][Panorama]
	- [**static** Panorama.parseUrl( _url, l, s, y, x_ )](#static-panoramaparseurl-url-l-s-y-x-)
	- [new Panorama( _container, config_ )](#new-panorama-container-config-)
	- [panorama.camera](#panoramacamera)
	- [panorama.controls](#panoramacontrols)
	- [panorama.raycasts](#panoramaraycasts)
	- [panorama.domElement](#panoramadomelement)
	- [panorama.domRect](#panoramadomrect)
	- [panorama.enabled](#panoramaenabled)
	- [panorama.id](#panoramaid)
	- [panorama.layers](#panoramalayers)
	- [panorama.renderer](#panoramarenderer)
	- [panorama.scene](#panoramascene)
	- [panorama.toLoad](#panoramatoload)
	- [panorama.resize()](#panoramaresize)
	- [panorama.load( _config_ ) **async**](#panoramaload-config--async)
	- [panorama.loadControls( _controls_ ) **async**](#panoramaloadcontrols-controls--async)
	- [panorama.loadBackground( _background_ ) **async**](#panoramaloadbackground-background--async)
	- [panorama.loadChildren( _children_ ) **async**](#panoramaloadchildren-children--async)
	- [panorama.dispose()](#panoramadispose)
	- [**Event**: 'resize'](#event-resize)
	- [**Event**: 'loadstart'](#event-loadstart)
	- [**Event**: 'controls-load'](#event-controls-load)
	- [**Event**: 'background-load'](#event-background-load)
	- [**Event**: 'children-load'](#event-children-load)
	- [**Event**: 'loadend'](#event-loadend)
	- [**Event**: 'render'](#event-render)
	- [**Event**: 'destruct'](#event-destruct)
- [Class: **PanoramaObject**][PanoramaObject]
	- [panoramaObject.styleList](#panoramaobjectstylelist)
	- [panoramaObject.dataSet](#panoramaobjectdataset)
	- [panoramaObject.ignoreIntersect](#panoramaobjectignoreintersect)
	- [**Event**: 'touchstart'](#event-touchstart)
	- [**Event**: 'touchmove'](#event-touchmove)
	- [**Event**: 'touchend'](#event-touchend)
	- [**Event**: 'mousedown'](#event-mousedown)
	- [**Event**: 'mousemove'](#event-mousemove)
	- [**Event**: 'mouseup'](#event-mouseup)
	- [**Event**: 'mouseleave'](#event-mouseleave)
	- [**Event**: 'click'](#event-click)
	- [**Event**: 'dblclick'](#event-dblclick)
	- [**Event**: 'contextmenu'](#event-contextmenu)
	- [**Event**: 'wheel'](#event-wheel)
	- [**Event**: 'style-update'](#event-style-update)

## Installation
Use the [three.js](https://threejs.org/) 0.126.0 or newer.

> 📍 **Note**: You can change **"constructor name"**, **"root object"** and **"THREE object"** to avoid conflicts.

```html
<script src="..." init-name="'Panorama2'" init-root="top" init-three="THREE2"></script>
// new top.Panorama2(); used THREE2

<script src="..." init-root="window.ViewTools ||= {}"></script>
// new ViewTools.Panorama();

```

### Example
```html
<html>
<head>

<script src="https://unpkg.com/three@0.126.0/build/three.min.js"></script>
<script src="panorama.min.js"></script>

</head>
<body style="width: 100vw; height: 100vh; overflow: hidden; margin: 0;">

<script>

let config = {
	background: {
		layers: [
			{
				type: 'hdri',
				url: 'https://forum.affinity.serif.com/uploads/monthly_2019_12/AffinityHDR_tonemap.jpg.7f510b0da163b17db4c6405e5be3848b.jpg',
			},
		],
	},
};

new Pamorama( document.body, config );

// let panorama = new Pamorama();
// document.body.appendChild( panorama.domElement );
// panorama.resize();
// panorama.loadBackground( config.background );

</script>

</body>
</html>
```

## Class: **EventDispatcher**
Event dispatcher.

### dispatcher.addEventListener( _type, callback_ )
- type [`<string>`][string] - The type of event to listen to.
- callback [`<function>`][function] - The function that gets called when the event is fired.

Adds a listener to an event type.

### dispatcher.removeEventListener( _type, callback_ )
- type [`<string>`][string] - The type of the listener that gets removed.
- callback [`<function>`][function] - The listener function that gets removed.

Removes a listener from an event type.

### dispatcher.hasEventListener( _type, callback_ )
- type [`<string>`][string] - The type of event to listen to.
- callback [`<function>`][function] - The function that gets called when the event is fired.

Checks if listener is added to an event type.

### dispatcher.dispatchEvent( _event_ )
- event [`<string>`][string] | [`<object>`][object] - The event that gets fired.

Fire an event type.


## Class: **Controls**
Panorama camera controls.

### [**static**][static] Controls.default
- [`<object>`][object]

Default properties of controls.

### controls.rotateMouseButton
- [`<integer>`][integer] - Button number left = 0, middle = 1, right = 2... **Default**: `0`.

Mouse button to camera rotate.

### controls.rotateTouchCount
- [`<integer>`][integer] - Count of touchs. **Default**: `1`.

Touchs count to camera rotate.

### controls.keys
- [`<object>`][object]
	- left [`<string>`][string] | [`<integer>`][integer] - **Default**: `'ArrowLeft'`.
	- right [`<string>`][string] | [`<integer>`][integer] - **Default**: `'ArrowRight'`.
	- up [`<string>`][string] | [`<integer>`][integer] - **Default**: `'ArrowUp'`.
	- down [`<string>`][string] | [`<integer>`][integer] - **Default**: `'ArrowDown'`.
	- zoom [`<string>`][string] | [`<integer>`][integer] - **Default**: `'Equal'`.
	- unzoom [`<string>`][string] | [`<integer>`][integer] - **Default**: `'Minus'`.

Keyboard keys controls.

### controls.azimuthAngle
- [`<number>`][number] - Number of radians. **Default**: `0`.

Camera start horizontal position.

### controls.minAzimuthAngle
- [`<number>`][number] | `null` - Number of radians. **Default**: `null` no limit.

Left limit of camera rotate.

### controls.maxAzimuthAngle
- [`<number>`][number] | `null` - Number of radians. **Default**: `null` no limit.

Right limit of camera rotate.

### controls.polarAngle
- [`<number>`][number] - Number of radians. **Default**: `Math.PI / 2`.

Camera start vertical position.

### controls.minPolarAngle
- [`<number>`][number] | `null` - Number of radians. **Default**: `null` no limit.

Up limit of camera rotate.

### controls.maxPolarAngle
- [`<number>`][number] | `null` - Number of radians. **Default**: `null` no limit.

Down limit of camera rotate.

### controls.fov
- [`<number>`][number] - **Default**: `70`.

Camera start field of view.

### controls.minFov
- [`<number>`][number] - **Default**: `10`.

Minimum limit of camera field of view. ( maximum zoom )

### controls.maxFov
- [`<number>`][number] - **Default**: `120`.

Maximum limit of camera field of view. ( minimum zoom )

### controls.autoRotate
- [`<number>`][number] - Number of radians per second. **Default**: `0` no rotation.

Camera auto rotation.

### controls.enabled
- [`<boolean>`][boolean] - **Default**: `true`.

Controls enabled / disabled.

### controls.zoomEnabled
- [`<boolean>`][boolean] - **Default**: `true`.

Zoom controls enabled / disabled.

### controls.rotateEnabled
- [`<boolean>`][boolean] - **Default**: `true`.

Rotation controls enabled / disabled.

### controls.wheelEnabled
- [`<boolean>`][boolean] - **Default**: `true`.

Mouse wheel controls enabled / disabled.

### controls.pointerEnabled
- [`<boolean>`][boolean] - **Default**: `true`.

Mouse pointer controls enabled / disabled.

### controls.keyboardEnabled
- [`<boolean>`][boolean] - **Default**: `true`.

Keyboard controls enabled / disabled.

### controls.dispose()
Destroy and remove all event listeners. 

### controls.setZoom( _val, force_ )
- val [`<number>`][number] - Value of zoom.
- force ? [`<boolean>`][boolean] - Ignore controls.zoomEnabled. **Default**: `false`.

Change camera zoom.

### controls.zoom( _val, force_ )
- val [`<number>`][number] - Value of add zoom.
- force ? [`<boolean>`][boolean] - Ignore controls.zoomEnabled. **Default**: `false`.

Change camera zoom.

### controls.setRotate( _theta, phi, force_ )
- theta [`<number>`][number] - Value of theta.
- phi [`<number>`][number] - Value of phi.
- force ? [`<boolean>`][boolean] - Ignore controls.rotateEnabled. **Default**: `false`.

Change camera rotation.

### controls.rotate( _theta, phi, force_ )
- theta [`<number>`][number] - Value of add theta.
- phi [`<number>`][number] - Value of add phi.
- force ? [`<boolean>`][boolean] - Ignore controls.rotateEnabled. **Default**: `false`.

Change camera rotation.

### controls.reset()
Reset camera params to default.

## Class: **Raycasts**
Panorama raycaster.

### raycasts.one
- [`<boolean>`][boolean] - **Default**: `true`.

Multy raycasting.

### raycasts.enabled
- [`<boolean>`][boolean] - **Default**: `true`.

Raycasts enabled / disabled.

### raycasts.dispose()
Destroy remove all event listeners. 

### raycasts.getIntersects( _pos_ )
- pos ? [`<object>`][object] - **Default**: `{ x: 0, y: 0 }`.
	- x [`<number>`][number] - Position of viewbox from left ( -1 ) to right ( 1 ).
	- y [`<number>`][number] - Position of viewbox from top ( 1 ) to bottom ( -1 ).

## Class: **Panorama** extends [**EventDispatcher**][EventDispatcher]
Panorama view.

> ❗ **Warning**: always call [`panorama.dispatch()`](#panoramadispatch) to destroy panorama.
> ❗ **Warning**: always call [`panorama.resize()`](#panoramaresize) after change [`panorama.domElement`](#panoramadomelement)parent element.

### [**static**][static] Panorama.parseUrl( _url, l, s, y, x_ )
- url [`<string>`][string] - Pattern.
- l [`<integer>`][integer] - Layer.
- s [`<integer>`][integer] - Side.
- y [`<integer>`][integer] - Row.
- x [`<integer>`][integer] - Column.
- _**Returns**_ [`<string>`][string] - Url.

Pattern url parser.


### new Panorama( _container, config_ )
- container ? [`<HTMLElement>`][HTMLElement] - Panorama place element. **Default**: `undefined`.
- config ? [`<object>`][object] - See [panorama.load()](#panoramaload-config--async). **Default**: `undefined`.

### panorama.camera
- [`<THREE.PerspectiveCamera>`][THREE.PerspectiveCamera]

### panorama.controls
- [`<Controls>`][Controls]

### panorama.raycasts
- [`<Raycasts>`][Raycasts]

### panorama.domElement
- [`<HTMLDivElement>`][HTMLDivElement]

### panorama.domRect
- [`<DOMRect>`][DOMRect]

### panorama.enabled
- [`<boolean>`][boolean] - **Default**: `true`.

Canorama enabled / disabled.

### panorama.id
- [`<integer>`][integer] - **Default**: Auto increment of Panorama constructor.

### panorama.layers
- [`<array>`][array]
	- [`<THREE.Scene>`][THREE.Scene]

### panorama.renderer
- [`<THREE.WebGLRenderer>`][THREE.WebGLRenderer]

### panorama.scene
- [`<THREE.Scene>`][THREE.Scene]

### panorama.toLoad
- [`<Set>`][Set]
	- [`<THREE.Mesh>`][THREE.Mesh]

Background fragments that hit the camera.

### panorama.resize()
Update camera asspect and [panorama.domRect](#panoramadomrect).

### panorama.load( _config_ ) [**async**][async]
- config [`<object>`][object]
	- controls [`<object>`][object] - See [panorama.loadControls()](#panoramaloadcontrols-controls--async).
	- background [`<object>`][object] - See [panorama.loadBackground()](#panoramaloadbackground-background--async).
	- children [`<array>`][array] - See [panorama.loadChildren()](#panoramaloadchildren-children--async).

Config loader.

### panorama.loadControls( _controls_ ) [**async**][async]
- controls [`<object>`][object]
	- rotateMouseButton ? [`<integer>`][integer] - See [controls.rotateMouseButton](#controlsrotatemousebutton).
	- rotateTouchCount ? [`<integer>`][integer] - See [controls.rotateTouchCount](#controlsrotatetouchcount).
	- keys ? [`<object>`][object] - See [controls.keys](#controlskeys).
	- azimuthAngle ? [`<number>`][number] - See [controls.azimuthAngle](#controlsazimuthangle).
	- minAzimuthAngle ? [`<number>`][number] | `null` - See [controls.minAzimuthAngle](#controlsminazimuthangle).
	- maxAzimuthAngle ? [`<number>`][number] | `null` - See [controls.maxAzimuthAngle](#controlsmaxazimuthangle).
	- polarAngle ? [`<number>`][number] - See [controls.polarAngle](#controlspolarangle).
	- minPolarAngle ? [`<number>`][number] | `null` - See [controls.minPolarAngle](#controlsminpolarangle).
	- maxPolarAngle ? [`<number>`][number] | `null` - See [controls.maxPolarAngle](#controlsmaxpolarangle).
	- fov ? [`<number>`][number] - See [controls.fov](#controlsfov).
	- minFov ? [`<number>`][number] - See [controls.minFov](#controlsminfov).
	- maxFov ? [`<number>`][number] - See [controls.maxFov](#controlsmaxfov).
	- autoRotate ? [`<number>`][number] - See [controls.autoRotate](#controlsautorotate).
	- enabled ? [`<boolean>`][boolean] - See [controls.enabled](#controlsenabled).
	- zoomEnabled ? [`<boolean>`][boolean] - See [controls.zoomEnabled](#controlszoomenabled).
	- rotateEnabled ? [`<boolean>`][boolean] - See [controls.rotateEnabled](#controlsrotateenabled).
	- wheelEnabled ? [`<boolean>`][boolean] - See [controls.wheelEnabled](#controlswheelenabled).
	- pointerEnabled ? [`<boolean>`][boolean] - See [controls.pointerEnabled](#controlspointerenabled).
	- keyboardEnabled ? [`<boolean>`][boolean] - See [controls.keyboardEnabled](#controlskeyboardenabled).

Controls config loader.

### panorama.loadBackground( _background_ ) [**async**][async]
- background [`<object>`][object]
	- url ? [`<string>`][string] - Image global url pattern. **Default**: `undefined`.
	- layers ? [`<array>`][array] - **Default**: `[ { url: background.url } ]`.
		- [`<object>`][object]
			- url ? [`<string>`][string] - Image url pattern. **Default**: Use global url.
			- type ? [`<string>`][string] - `'hdri'` | `'sphere'`, `'cubemap'`, `'skybox'`. **Default**: `'hdri'`.
			- count ? [`<integer>`][integer] - Count of pieces. **Default**: `undefined`.

Background config loader.

### panorama.loadChildren( _children_ ) [**async**][async]
- children [`<array>`][array]
	- [`<PanoramaObject>`][PanoramaObject]

Children config loader.

### panorama.dispose()
Destroy remove all event listeners. 

### **Event**: 'resize'

### **Event**: 'loadstart'
Fire before [panorama.load()](#panoramaload-config--async).

### **Event**: 'controls-load'

### **Event**: 'background-load'

### **Event**: 'children-load'

### **Event**: 'loadend'
Fire after [panorama.load()](#panoramaload-config--async).

### **Event**: 'render'

### **Event**: 'destruct'
Fire after [panorama.dispose()](#panoramadispose).

## Class: **PanoramaObject** extends [**THREE.Object3D**][THREE.Object3D]
Panorama custom objects

### panoramaObject.styleList
- [`<Set>`][Set]
	- [`<string>`][string]

### panoramaObject.dataSet
- _[`<Map>`][Map]_
	- [`<string>`][string]: [`<any>`][any]

### panoramaObject.ignoreIntersect
- [`<boolean>`][boolean]

### **Event**: 'touchstart'

### **Event**: 'touchmove'

### **Event**: 'touchend'

### **Event**: 'mousedown'

### **Event**: 'mousemove'

### **Event**: 'mouseup'

### **Event**: 'mouseleave'

### **Event**: 'click'

### **Event**: 'dblclick'

### **Event**: 'contextmenu'

### **Event**: 'wheel'

### **Event**: 'style-update'
Fire after [panoramaObject.styleList](#panoramaobjectstylelist) or [panoramaObject.dataSet](#panoramaobjectdataset) change.



[function]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Functions>
[object]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object>
[string]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String>
[boolean]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Boolean>
[number]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number>
[integer]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isInteger>
[array]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array>
[any]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/typeof>

[async]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/async_function>
[static]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Classes/static>

[Set]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Set>
[Map]: <https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map>
[DOMRect]: <https://developer.mozilla.org/en-US/docs/Web/API/DOMRect>
[HTMLElement]: <https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement>
[HTMLDivElement]: <https://developer.mozilla.org/en-US/docs/Web/API/HTMLDivElement>

[THREE.Object3D]: <https://threejs.org/docs/?q=Mesh#api/en/core/Object3D>
[THREE.Mesh]: <https://threejs.org/docs/?q=Mesh#api/en/objects/Mesh>
[THREE.Scene]: <https://threejs.org/docs/?q=Scene#api/en/scenes/Scene>
[THREE.WebGLRenderer]: <https://threejs.org/docs/?q=WebGLRenderer#api/en/renderers/WebGLRenderer>
[THREE.PerspectiveCamera]: <https://threejs.org/docs/#api/en/cameras/PerspectiveCamera>

[EventDispatcher]: <#class-eventdispatcher>
[Controls]: <#class-controls>
[Raycasts]: <#class-raycasts>
[Panorama]: <#class-panorama-extends-eventdispatcher>
[PanoramaObject]: <#class-panoramaobject-extends-threeobject3d>
