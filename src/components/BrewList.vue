<template lang="html">
  <div class="card brew-list">
    <ul class="list-group list-group-flush">
      <li
       @mouseover="mouseOver(index)"
       @mouseleave="mouseLeave(index)"
       :key="index"
       v-for="(brew, index) in brews"

      class="list-group-item"

      >{{brew.name}}, {{brew.state}}</li>

    </ul>
  </div>
</template>

<script>
  export default {
    name: "BrewList",
    props: {
      brews: Array
    },
    methods: {
      mouseOver: function(index) {
        this.$emit('mouse-over-brew', index);
      },
      mouseLeave: function(index) {
        this.$emit('mouse-leave-brew', index);
      },
    }
  }
</script>

<style lang="scss">
  .brew-list {
    height: 80vh;
    overflow-y: scroll;
    li {
      &:hover {
        background-color: darkgrey;
      }
    }
  }
</style>
