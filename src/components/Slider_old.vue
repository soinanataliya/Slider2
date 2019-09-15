<template>
<div>
    <div class="container">
        <div @click="changeSlideBack" class="container__arrow--back"><i class="left"></i></div>
        <div class="container__content">
            <transition name="slide">
                  <div v-if="visibleSlide === 1" class="container__content__slide1"></div>
            </transition>
            <transition name="slide">
                <div v-if="visibleSlide === 2" class="container__content__slide2"></div>
            </transition>
            <transition name="slide">
            <div v-if="visibleSlide === 3" class="container__content__slide3"></div>
            </transition>
            </div>
        <div @click="changeSlideForward" class="container__arrow--forward"><i class="right"></i></div>
     </div>
     <div class="dots">
      <div v-for="(slide, index) in allSlides" :key="index" class="dots__dot" @click="slideClickChange(index)"></div>
     </div>
</div>
</template>
<script>
export default {
  name: 'SliderOld',
  methods: {
    changeSlideForward () {
      this.visibleSlide < this.allSlides.length ? this.visibleSlide++ : this.visibleSlide = 1
    },
    changeSlideBack () {
      this.visibleSlide > 1 ? this.visibleSlide-- : this.visibleSlide = this.allSlides.length
    },
    slideClickChange (value) {
      console.log(value)
      this.visibleSlide = value + 1
    }
  },
  mounted () {
    this.slideNumber = this.allSlides.length
  },
  data () {
    return {
      visibleSlide: 1,
      allSlides: [1, 2, 3],
      slideNumber: null
    }
  }
}
</script>
 <style lang="scss" scoped>
    .container {
        height: 420px;
        background-color: teal;
        display: flex;
        justify-content: center;
        align-items: center;
        flex-wrap: row nowrap;
    &__content {
        overflow: hidden;
        position: relative;
        background-color: teal;
        width: 400px;
        height: 400px;
        z-index: 100;
        &__slide1 {
            background-image: url('../assets/1.jpg');
            width: 400px;
            height: 400px;
            position: absolute;
            top: 20;
        }
        &__slide2 {
            background-image: url('../assets/2.jpg');
            width: 400px;
            height: 400px;
            position: absolute;
            top: 20;
        }
        &__slide3 {
            background-image: url('../assets/3.jpg');
            width: 400px;
            height: 400px;
            position: absolute;
            top: 20;
        }
    }
&__arrow--forward {
        padding: 25px;
        cursor: pointer;
    }
&__arrow--back {
        padding: 25px;
        cursor: pointer;
    }
}
.dots {
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        background-color: teal;
        &__dot {
        width: 10px;
        height: 10px;
        background-color: black;
        border-radius: 50%;
        margin: 10px 10px;
        &:hover {
            background-color: aliceblue;
        }
    }
}

.slide-leave-active,
.slide-enter-active {
  transition: 1s;
}
.slide-enter {
  transform: translate(100%, 0);
}
.slide-leave-to {
  transform: translate(-100%, 0);
}

i {
  border: solid black;
  border-width: 0 10px 10px 0;
  display: inline-block;
  padding: 10px;
}
.right {
  transform: rotate(-45deg);
  -webkit-transform: rotate(-45deg);
  &:hover{
      border: solid aliceblue;
      border-width: 0 10px 10px 0;
      display: inline-block;
      padding: 10px;
  }
}
.left {
  transform: rotate(135deg);
  -webkit-transform: rotate(135deg);
   &:hover{
      border: solid aliceblue;
      border-width: 0 10px 10px 0;
      display: inline-block;
      padding: 10px;
  }
}

 </style>
