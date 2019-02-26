<template>
  <div class="animation">
    <div :ref="aniConf.name"></div>
  </div>
</template>

<script>
import bodymovin from 'lottie-web';

export default {
  name: 'animation',
  data () {
    return {
      animation: null
    }
  },
  props: {
    aniConf: {
        type: Object,
        required: true,
        default: function () {
            return {
                name: 'robot',
                data: require('../../public/json/data1.json')
            }
        }
    }
  },
  components: {},
  mounted () {
      console.log(this.props)
      let vm  = this
      let element = vm.$refs[vm.aniConf.name]
      let data = vm.aniConf.data
      
      vm.animation = bodymovin.loadAnimation({
            container: element, // Required
            animationData: data, // Required
            renderer: 'svg', // Required
            loop: true, // Optional
            autoplay: true // Optional
          })
  }
}
</script>

<style lang="scss" scoped>
.animation {
    
}
</style>
