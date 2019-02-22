<template>
  <div id="app">
    <slick
      ref="slick"
      :options="slickOptions"
      @afterChange="handleAfterChange"
      @beforeChange="handleBeforeChange"
      @breakpoint="handleBreakpoint"
      @destroy="handleDestroy"
      @edge="handleEdge"
      @init="handleInit"
      @reInit="handleReInit"
      @setPosition="handleSetPosition"
      @swipe="handleSwipe"
      @lazyLoaded="handleLazyLoaded"
      @lazyLoadError="handleLazeLoadError">
      <div class="card-wrapper" :key="card.id" v-for="card in cards">
        <div  class="card-animation">
          <animation :ani-conf="card.conf"></animation>
        </div>
        <div class="card-content">
          <h5>你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？</h5>
          <input type="radio" id="one" value="first" v-model="picked">
          <label for="one">Yes</label>
          <input type="radio" id="two" value="seconed" v-model="picked">
          <label for="two">No</label>
        </div>
      </div>
      <!-- <div class="card-wrapper" :key="card.id" v-for="card in cards">
        <div class="card-animation">
          <div class="animation" :ref="card.element"></div>
        </div>
        <div class="card-content">
          <h5>{{ card.question }}</h5>
          <input type="radio" id="one" :value="card.value1" v-model="card.picked">
          <label for="one">Yes</label>
          <input type="radio" id="two" :value="card.value2" v-model="card.picked">
          <label for="two">No</label>
        </div>
      </div> -->
      <!-- <div class="card-wrapper">
        <div class="card-animation">
          <div class="animation" :ref="robot1"></div>
        </div>
        <div class="card-content">
          <h5>你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？</h5>
          <input type="radio" id="one" value="first" v-model="picked">
          <label for="one">Yes</label>
          <input type="radio" id="two" value="seconed" v-model="picked">
          <label for="two">No</label>
        </div>
      </div>
      <div class="card-wrapper">
        <div class="card-animation">
          <div class="animation" ref="robot2"></div>
        </div>
        <div class="card-content">
          <h5>你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？</h5>
          <input type="radio" id="one" value="third" v-model="picked">
          <label for="one">Yes</label>
          <input type="radio" id="two" value="forth" v-model="picked">
          <label for="two">No</label>
        </div>
      </div>
      <div class="card-wrapper">
        <div class="card-animation">
          <div class="animation" ref="robot3"></div>
        </div>
        <div class="card-content">
          <h5>你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？</h5>
          <input type="radio" id="one" value="fifth" v-model="picked">
          <label for="one">Yes</label>
          <input type="radio" id="two" value="sixth" v-model="picked">
          <label for="two">No</label>
        </div>
      </div> -->
    </slick>
  </div>
</template>

<script>
import Animation from './components/animation.vue'
import Slick from 'vue-slick';
import axios from 'axios'
import bodymovin from 'lottie-web';


export default {
  name: 'app',
  data () {
    return {
      cover: '',
      steps: 0,
      publicPath: process.env.BASE_URL,
      picked: true,
      isFold: false,
      picked: '',
      robot1: 'robot1',
      ansmers: [

      ],
      cards: [
        {
          id: 'card1',
          conf: {
            name: 'robot',
            data: require('../public/data1.json')
          },
          name: 'card1',
          element: 'robot1',
          question: '你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？',
          value1: 0,
          value2: 1,
          picked: ''
        },
        {
          id: 'card2',
          conf: {
            name: 'robot2',
            data: require('../public/data2.json')
          },
          name: 'card2',
          element: 'robot2',
          question: '你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？',
          value1: 0,
          value2: 1,
          picked: ''
        },
        {
          id: 'card3',
          conf: {
            name: 'robot3',
            data: require('../public/data3.json')
          },
          name: 'card3',
          element: 'robot3',
          question: '你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？',
          value1: 0,
          value2: 1,
          picked: ''
        },
      ],
      slickOptions: {
          slidesToShow: 1,
          dots: true,
          centerMode: true,
          arrows: false,
          infinite: false,
          responsive: [
            {
              breakpoint: 768,
              settings: {
                arrows: false,
                centerMode: true,
                centerPadding: '40px',
                slidesToShow: 3
              }
            },
            {
              breakpoint: 480,
              settings: {
                arrows: false,
                centerMode: true,
                centerPadding: '30px',
                slidesToShow: 1
              }
            }
          ]
          // Any other options that can be got from plugin documentation
      }
    }
  },
  mounted(){

      let vm  = this
      // let element1 = this.$refs['robot1']
      // let element2 = this.$refs['robot2']
      // let element3 = this.$refs['robot3']
      
      // this.animation1 = bodymovin.loadAnimation({
      //       container: element1, // Required
      //       animationData: animationData1, // Required
      //       renderer: 'svg', // Required
      //       loop: true, // Optional
      //       autoplay: true, // Optional
      //       name: "Hello World", // Name for future reference. Optional.
      //     })

      // this.animation2 = bodymovin.loadAnimation({
      //       container: element2, // Required
      //       animationData: animationData2, // Required
      //       renderer: 'svg', // Required
      //       loop: true, // Optional
      //       autoplay: true, // Optional
      //       name: "Hello World", // Name for future reference. Optional.
      //     })

      // this.animation3 = bodymovin.loadAnimation({
      //       container: element3, // Required
      //       animationData: animationData3, // Required
      //       renderer: 'svg', // Required
      //       loop: true, // Optional
      //       autoplay: true, // Optional
      //       name: "Hello World", // Name for future reference. Optional.
      //     })
      // this.animation1.stop()
      // this.animation2.stop()
      // this.animation3.stop()
    },
  watch: {
    cards: {
      handler: function(newValue) {
          console.log(newValue.picked)
      },
      deep: true
    }
  },
  components: {
    HelloWorld,
    Slick,
    Animation
  },
  methods: {
        controlAni () {
          console.log("hello")
          
        },
        next() {
          console.log("helll next")
          
            this.$refs.slick.next();
        },

        prev() {
            this.$refs.slick.prev();
        },

        reInit() {
            // Helpful if you have to deal with v-for to update dynamic lists
            this.$nextTick(() => {
                this.$refs.slick.reSlick();
            });
        },
        // Events listeners
        handleAfterChange(event, slick, currentSlide) {
            console.log('handleAfterChange', event, slick, currentSlide);
        },
        handleBeforeChange(event, slick, currentSlide, nextSlide) {
          this.isFold = false
            console.log('handleBeforeChange', event, slick, currentSlide, nextSlide);
        },
        handleBreakpoint(event, slick, breakpoint) {
            console.log('handleBreakpoint', event, slick, breakpoint);
        },
        handleDestroy(event, slick) {
            console.log('handleDestroy', event, slick);
        },
        handleEdge(event, slick, direction) {
            console.log('handleEdge', event, slick, direction);
        },
        handleInit(event, slick) {
            console.log('handleInit', event, slick);
        },
        handleReInit(event, slick) {
            console.log('handleReInit', event, slick);
        },
        handleSetPosition(event, slick) {
            console.log('handleSetPosition', event, slick);
        },
        handleSwipe(event, slick, direction) {
            console.log('handleSwipe', event, slick, direction);
        },
        handleLazyLoaded(event, slick, image, imageSource) {
            console.log('handleLazyLoaded', event, slick, image, imageSource);
        },
        handleLazeLoadError(event, slick, image, imageSource) {
            console.log('handleLazeLoadError', event, slick, image, imageSource);
        },
        expand() {
          this.isFold = !this.isFold
        }
    }
}
</script>

<style lang="scss">
@import '../node_modules/slick-carousel/slick/slick.css';

html, body {
  margin: 0;
  padding: 0;
}
#app {
  .slick-slide {
    width: 80vw;
  }
  .card-wrapper {
    min-height: 100vh;
    position: relative;
    .card-animation {
      width: 95%;
      height: 40vh;
    }
    .card-content {
      position: absolute;
      left: 50%;
      transform: translateX(-50%);
      margin: 0;
      box-sizing: border-box;
      padding: 10px;
      width: 95%;
      min-height: 40vh;
      border: solid 1px black;
      border-radius: 5px;
      margin: 0;
      h5 {
        margin: 0;
      }
    }
  }
}
</style>
