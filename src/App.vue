<template>
  <div id="app">

    <div class="game-box">
      <div class="animation-wrapper">
        <div class="animation-control" v-show="step === index" :key="index" v-for="(item, index) in animations">
          <animation :ani-conf="item"></animation>
        </div>
      </div>
      <div class="slick-wrapper">
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
            <div class="card-content">
              <h5 class="card-title">你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？</h5>
              <input type="radio" id="one" value="first" v-model="picked">
              <label for="one">Yes</label>
              <input type="radio" id="two" value="seconed" v-model="picked">
              <label for="two">No</label>
              <div class="extend-wrapper">
                <button class="next">
                  下一題
                </button>
                <div class="give-up">放棄遊戲看結果</div>
                <h5 class="card-subtitle">別人怎麼選?</h5>
                <p>到目前為止，63%的使用者跟你的答案相同。</p>
                <div class="card-chart">
                  <single-chart :option-type="card.chart.type" :option-title="card.chart.option1" :option-number="card.chart.number1"></single-chart>
                  <single-chart :option-type="card.chart.type" :option-title="card.chart.option2" :option-number="card.chart.number2"></single-chart>
                </div>
                <h5 class="card-subtitle">專家怎麼說?</h5>
                <h5 class="card-subtitle">延伸閱讀</h5>
              </div>
            </div>
          </div>
        </slick>
      </div>
    </div>
    
  </div>
</template>

<script>
import Animation from './components/animation.vue'
import SingleChart from './components/singleChart.vue'
import Slick from 'vue-slick';
import axios from 'axios'
import bodymovin from 'lottie-web';


export default {
  name: 'app',
  data () {
    return {
      cover: '',
      step: 0,
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
            data: require('../public/json/data1.json')
          },
          chart: {
            type: 'text',
            option1: '是',
            number1: 10,
            option2: '否',
            number2: 90
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
            data: require('../public/json/data2.json')
          },
          chart: {
            type: 'star',
            number1: 1,
            number2: 5
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
            data: require('../public/json/data3.json')
          },
          chart: {
            type: 'text',
            option1: '是',
            number1: 40,
            option2: '否',
            number2: 60
          },
          name: 'card3',
          element: 'robot3',
          question: '你曾經為了拿LINE免費貼圖，分享活動訊息給親朋好友嗎？',
          value1: 0,
          value2: 1,
          picked: ''
        },
      ],
      animations : [
        {
          name: 'robot',
          data: require('../public/json/data1.json')
        },
        {
          name: 'robot2',
          data: require('../public/json/data2.json')
        },
        {
          name: 'robot3',
          data: require('../public/json/data3.json')
        }
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
    Slick,
    Animation,
    SingleChart
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
          this.step = nextSlide

          // this.isFold = false
          // let newAnimation = {}
          // newAnimation = { ...this.cards[nextSlide].conf }
          // this.currentAnimations = { ...newAnimation }
          
        console.log("currentSlider:" + currentSlide)
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
    },
}
</script>

<style lang="scss">
@import '../node_modules/slick-carousel/slick/slick.css';

html, body {
  margin: 0;
  padding: 0;
}
#app {

  .game-box {
    .animation-wrapper {
      @media (min-width: 768px) and (max-width: 1024px){

      }
      @media screen and (min-width: 1025px){
        width: 50%;
        float: left;
      }
        .slick-slide {
          width: 100%;
        }
    }
    .slick-wrapper {
      @media (min-width: 768px) and (max-width: 1024px){

      }
      @media screen and (min-width: 1025px){
        width: 50%;
        float: right;
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
          .extend-wrapper {
            .next {
              width: 100%;
            }
          }       
        }
      }
    }
  }
  
  
}
</style>
