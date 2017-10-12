# VueSwing

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A Vue.js wrapper for [Swing](https://github.com/gajus/swing).

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
| Property | Type | Description |
|----------|------|-------------|
| config   | Object | Optional [Swing config](https://github.com/gajus/swing#configuration) |

## Events

VueSwing emits [every event Swing emits](https://github.com/gajus/swing#events)
