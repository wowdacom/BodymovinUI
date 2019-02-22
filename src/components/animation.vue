<template>
  <div class="animation">
    <div :ref="conf.name"></div>
  </div>
</template>

<script>
import bodymovin from 'lottie-web';

export default {
  name: 'App',
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
                data: require('../../public/data1.json')
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
