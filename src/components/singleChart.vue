<template>
  <div class="single-chart">
    <div class="title-wrapper">
      <template v-if="optionType === 'text'">
        <div class="option-title">{{ optionTitle }}</div>
      </template>
      <template v-if="optionType === 'star'">
        <div class="option-title">
          <ul class="stars">
            <li class="star" :key="item" v-for="item in optionNumber">
              <img :src="star" alt="">
            </li>
          </ul>
        </div>
      </template>
      <div class="option-number">{{ barWidth + '%' }}</div>
    </div>
    <div class="chart-bar-wrapper">
      <div class="chat-bar" :style="{'width': barWidth + '%'}"></div>
    </div>
  </div>
</template>

<script>
import bodymovin from 'lottie-web';

export default {
  name: 'animation',
  data () {
    return {
      star: require("../../public/icons/star.svg")
    }
  },
  props: {
    optionType: {
      type: String,
      default: 'text'
    },
    optionTitle: {
      type: String,
      default: '是'
    },
    optionNumber: {
      type: Number,
      default: 0
    }
  },
  components: {},
  computed: {
    barWidth () {
      if (this.optionType === 'star') {
        return this.optionNumber * (100 / 5)
      } else {
        return this.optionNumber
      }
    }
  },
  mounted () {
    console.log(this.$props)
  }
}
</script>

<style lang="scss" scoped>
.single-chart {
  width: 100%;
    .title-wrapper {
      width: 100%;
      &:after {
          clear:both;
          content:" ";
          display:block;
      }
      .option-title {
        float: left;
        .stars {
          margin: 0;
          padding: 0;
          .star {
            display: inline-block;
            img {
              width: 18px;
            }
          }
        }
      }
      .option-number {
        float: right;
      }
    }
    .chart-bar-wrapper {
      width: 100%;
      height: 8px;
      background-color: #465362;
      .chat-bar {
        height: inherit;
        background-color: #ffce0c;
      }
    }
}
</style>
