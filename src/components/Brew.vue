<template>
  <div class="container-fluid">
    <div class="container">
      <div class="row">
        <div class="col-12">
          <h1 class="text-center text-info">breweries</h1>
        </div>
        <!-- /.col-12 -->
      </div>
      <!-- /.row -->
      <div class="row">
        <div class="col-6 brew-list">
          <BrewList
          @mouse-over-brew="mouseOverBrew"
          @mouse-leave-brew="mouseLeaveBrew"
          :brews="brews"/>
        </div>
        <div class="col-6">
          <BrewMap :brews="brews"/>
        </div>
      </div>
      </div>
    </div>
    <!-- /.container -->
</template>

<script>
import axios from 'axios'
import BrewList from './BrewList.vue'
import BrewMap from './BrewMap.vue'
export default {
  name: 'Brew',
  components: {BrewMap, BrewList},
  data: function () {
    return {
      brews: [],
      normalIconSize: [20,20],
      largeIconSize: [50,50]
    }
  },

  mounted: function () {
    axios.get('https://api.openbrewerydb.org/breweries')
      .then((r) => {
        this.brews = r.data.filter(r => r.state == 'Arizona')
        .map(r => {
          r.iconSize = this.normalIconSize;
          return r;
        });
      })
  },
  methods: {
    mouseOverBrew: function(index) {
      this.brews[index].iconSize = this.largeIconSize;
    },
    mouseLeaveBrew: function(index) {
      this.brews[index].iconSize = this.normalIconSize;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss" scoped>

</style>
