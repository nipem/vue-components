<template>
  <div id="app">
    <h2>Swiper component</h2>
    <hr>

    <div class="flex flex-wrap justify-around">
      <section>
        <h2>default Transition Classes: fadeIn</h2>
        <swiper class="knpm-swiper"
          direction="vertical"
          :prevTransition="{
            'enter-active-class': 'animated fadeIn',
            'leave-active-class': 'animated fadeOut',
          }"
          :nextTransition="{
            'enter-active-class': 'animated fadeIn',
            'leave-active-class': 'animated fadeOut',
          }"
          >
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>
        </swiper>
      </section>

      <section>
        <h2>Custom Transition Classes: fadeIn-X</h2>
        <swiper class="knpm-swiper"
          :prevTransition="{
            'enter-active-class': 'animated fadeInLeft',
            'leave-active-class': 'animated fadeOutRight',
          }"
          :nextTransition="{
            'enter-active-class': 'animated fadeInRight',
            'leave-active-class': 'animated fadeOutLeft',
          }"
          >
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>
        </swiper>
      </section>

      <section>
        <h2>Custom Transition Classes: fadeIn-Y</h2>
        <swiper class="knpm-swiper"
          direction="vertical"
          :prevTransition="{
            'enter-active-class': 'animated fadeInDown',
            'leave-active-class': 'animated fadeOutDown',
          }"
          :nextTransition="{
            'enter-active-class': 'animated fadeInUp',
            'leave-active-class': 'animated fadeOutUp',
          }"
          >
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>
        </swiper>
      </section>

      <section>
        <h2>loop: false</h2>
        <swiper class="knpm-swiper" :loop="false">
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>
        </swiper>
      </section>

      <section>
        <h2>autoplay: false</h2>
        <swiper class="knpm-swiper" :autoplay="false">
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>
        </swiper>
      </section>
      <section>
        <h2>navigationEnabled: true & paginationEnabled: true</h2>
        <p>active: {{active}}</p>
        <swiper ref="custom-swiper" class="knpm-swiper" :navigationEnabled="true" :paginationEnabled="true" v-model="active">
          <slide v-for="(image, index) of images" :key="index">
            <img :src="image" alt="" draggable="false">
          </slide>

          <div class="absolute w-full flex items-center justify-center bottom-0 mb-1" slot="pagination">
            <span>Custom pagination</span>
            <ul class="swiper-pagination w-auto relative bottom-0">
              <li
                v-for="(value, index) of images.length"
                :key="index"
                class="swiper-pagination__dot bg-blue-600"
                :class="index === active ? 'active' : ''"
                @click="changeActiveIndex(index)">
              </li>
            </ul>
          </div>
        </swiper>
      </section>
    </div>
  </div>
</template>

<script>
import { Swiper, Slide } from '../lib/'

const images = [
  'https://dummyimage.com/400x300/30e320',
  'https://dummyimage.com/400x300/144cdb',
  'https://dummyimage.com/400x300/db1414',
  'https://dummyimage.com/400x300/f5c72e'
]

export default {
  name: 'app',
  components: {
    Swiper,
    Slide
  },
  data () {
    return {
      images: [],
      active: 0
    }
  },
  created () {
    setTimeout(() => {
      this.images = images
    }, 2000)
  },
  methods: {
    changeActiveIndex (index) {
      this.$refs['custom-swiper'].changeActiveIndex(index)
    }
  }
}
</script>

<style lang="css">
/* @import url('../lib/transition/fade-in-x.css'); */
@import url('https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.2/animate.min.css');
@import url('https://cdn.bootcss.com/tailwindcss/1.1.2/utilities.min.css');
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.knpm-swiper {
  margin: auto;
  width: 400px;
  height: 300px;
}
h2 {
  text-align: center;
}
</style>
