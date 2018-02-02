<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
const Swing = require('swing')

export default {
  name: 'vue-swing',

  props: ['config'],

  data () {
    return {
      stack: null,
      cards: [],
      observer: null
    }
  },

  mounted () {
    this.stack = Swing.Stack(this.config || {})
    let children = [...this.$el.children]
    children.forEach(el => {
      this.cards.push(this.stack.createCard(el))
    })

    // Observe changes in DOM
    this.observer = new MutationObserver(mutations => {
      mutations.forEach(({ addedNodes }) =>
        addedNodes.forEach(el => {
          if (this.stack.getCard(el) == null) {
            this.cards.push(this.stack.createCard(el))
          }
        })
      )
    })
    this.observer.observe(this.$el, { childList: true })

    // Register events
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
      this.stack.on(event, e => {
        this.$emit(event, e)
      })
    }
  },

  beforeDestroy () {
    this.observer.disconnect()
  },

  Card: Swing.Card,
  Direction: Swing.Direction,
  Stack: Swing.Stack
}
</script>

<style>

</style>
