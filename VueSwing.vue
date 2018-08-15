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
    let children = Array.prototype.slice.call(this.$el.children)
    children.forEach(el => {
      this.cards.push(this.stack.createCard(el))
    })

    // Observe changes in DOM
    this.observer = new MutationObserver(mutations => {
      const addedElements = []
      const removedElements = []
      mutations.forEach(({ addedNodes, removedNodes }) => {
        addedElements.push(...addedNodes)
        removedElements.push(...removedNodes)
      })

      // Create a new card for each new element
      addedElements.forEach(el => {
        // Ignore if the added element is also removed
        const i = removedElements.indexOf(el)
        if (i !== -1) {
          removedElements.splice(i, 1)
          return
        }

        const card = this.stack.getCard(el)
        if (card == null) {
          this.cards.push(this.stack.createCard(el))
        }
      })

      // Remove the card if the element is gone
      removedElements.forEach(el => {
        const card = this.stack.getCard(el)
        if (card != null) {
          this.cards.splice(this.cards.indexOf(card), 1)
          this.stack.destroyCard(card)
        }
      })
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

