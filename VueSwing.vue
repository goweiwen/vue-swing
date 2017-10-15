<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
const Swing = require('swing')

export default {
  name: 'vue-swing',

  props: ['config']

  mounted () {
    const stack = Swing.Stack(this.config || {})

    const cards = []
    for (let el of this.$el.children) {
      cards.push(stack.createCard(el))
    }

    const events = [
      'throwout',
      'throwoutend',
      'throwoutdown',
      'throwoutleft',
      'throwoutright',
      'throwoutup',
      'throwin',
      'throwinend',
      'dragstart',
      'dragmove',
      'dragend',
      'destroyCard'
    ]

    for (let event of events) {
      stack.on(event, e => {
        this.$emit(event, e)
      })
    }
  },
}
</script>

<style>
</style>
