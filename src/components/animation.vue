<template>
  <div class="animation">
    <div ref="robot"></div>
  </div>
</template>

<script>
import bodymovin from 'lottie-web';

export default {
  name: 'App',
  data () {
    return {}
  },
  props: {
      
  },
  components: {},
  mounted () {
      let vm  = this
      let element = vm.$refs['robot']
      
      vm.animation1 = bodymovin.loadAnimation({
            container: element, // Required
            animationData: require('../../public/data1.json'), // Required
            renderer: 'svg', // Required
            loop: false, // Optional
            autoplay: false // Optional
          })
  }
}
</script>

<style lang="scss" scoped>
.animation {
    
}
</style>
