# VueSwing

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A Vue.js wrapper for [Swing](https://github.com/gajus/swing). Swing is a swipeable cards interface. The swipe-left/swipe-right for yes/no input. As seen in apps like Jelly and Tinder, and many others.

## Installing

```sh
npm install --save vue-swing
```

## Usage

```js
import VueSwing from 'vue-swing'

Vue.component('vue-swing', VueSwing)
```

```html
<vue-swing
  @throwout="throwout"
  @throwin="throwin"
  :config="config"
>
  <div class="box">Throw me!</div>
</vue-swing>
```

## Properties

VueSwing takes in one `config` Object, which can consist of any of these keys:

| Name | Description | Default |
| --- | --- | --- |
| `isThrowOut` | Invoked in the event of `dragend`. Determines if element is being thrown out of the stack. | Element is considered to be thrown out when `throwOutConfidence` is equal to 1. |
| `allowedDirections` | Array of directions in which cards can be thrown out. | [VueSwing.Direction.DOWN, VueSwing.Direction.LEFT, VueSwing.Direction.RIGHT, VueSwing.Direction.UP]. |
| `throwOutConfidence` | Invoked in the event of `dragmove`. Returns a value between 0 and 1 indicating the completeness of the throw out condition. | Ration of the absolute distance from the original card position and element width. |
| `throwOutDistance` | Invoked when card is added to the stack. The card is thrown to this offset from the stack. | The value is a random number between `minThrowOutDistance` and `maxThrowOutDistance`. |
| `minThrowOutDistance` | In effect when `throwOutDistance` is not overwritten. | 450. |
| `maxThrowOutDistance` | In effect when `throwOutDistance` is not overwritten. | 500. |
| `rotation` | Invoked in the event of `dragmove`. Determine the rotation of the element. | Rotation is equal to the proportion of horizontal and vertical offset times the `maximumRotation` constant. |
| `maxRotation` | In effect when `rotation` is not overwritten. | 20. |
| `transform` | Invoked in the event of `dragmove` and every time the physics solver is triggered. | Uses CSS transform to translate element position and rotation. |

For more information, look at [Swing's documentation](https://github.com/gajus/swing#configuration)

## Events

| Name            | Description                                                             |
| --------------- | ----------------------------------------------------------------------- |
| `throwout`      | When card has been thrown out of the stack.                             |
| `throwoutend`   | When card has been thrown out of the stack and the animation has ended. |
| `throwoutdown`  | Shorthand for `throwout` event in the `VueSwing.Direction.DOWN` direction.       |
| `throwoutleft`  | Shorthand for `throwout` event in the `VueSwing.Direction.LEFT` direction.       |
| `throwoutright` | Shorthand for `throwout` event in the `VueSwing.Direction.RIGHT` direction.      |
| `throwoutup`    | Shorthand for `throwout` event in the `VueSwing.Direction.UP` direction.         |
| `throwin`       | When card has been thrown into the stack.                               |
| `throwinend`    | When card has been thrown into the stack and the animation has ended.   |
| `dragstart`     | Hammer [panstart](http://hammerjs.github.io/recognizer-pan/).           |
| `dragmove`      | Hammer [panmove](http://hammerjs.github.io/recognizer-pan/).            |
| `dragend`       | Hammer [panend](http://hammerjs.github.io/recognizer-pan/).             |
| `destroyCard`   | When card.destroy calls stack.destroyCard.                              |

For more information, look at [Swing's documentation](https://github.com/gajus/swing#events)
