<template>
  <div>
    <slot></slot>
  </div>
</div>
</template>

<script>
const Swing = require('swing')

export default {
  mounted () {
    const stack = Swing.Stack(this.config || {})

    const card = stack.createCard(this.$el)

    card.on('throwout', event => { this.$emit('throwout', event) })
    card.on('throwoutend', event => { this.$emit('throwoutend', event) })
    card.on('throwoutdown', event => { this.$emit('throwoutdown', event) })
    card.on('throwoutleft', event => { this.$emit('throwoutleft', event) })
    card.on('throwoutright', event => { this.$emit('throwoutright', event) })
    card.on('throwoutup', event => { this.$emit('throwoutup', event) })
    card.on('throwin', event => { this.$emit('throwin', event) })
    card.on('throwinend', event => { this.$emit('throwinend', event) })
    card.on('dragstart', event => { this.$emit('dragstart', event) })
    card.on('dragmove', event => { this.$emit('dragmove', event) })
    card.on('dragend', event => { this.$emit('dragend', event) })
    card.on('destroyCard', event => { this.$emit('destroyCard', event) })
  },

  props: ['config']
}
</script>

<style>
</style>
