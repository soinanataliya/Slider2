<template>
  <div class="slider">
      <div class="slider__container container">
          <p @click="goBack" :class="{ delanimation: activeAnimation }" class="container__arrow"><i class="left"></i></p>
          <div class="container__content">
           <transition :name="animateName">
           <div class="container__slide" :key="currentItem">
            <img :src="currentImage">
           </div>
          </transition>
          </div>
          <p @click="goNext"  :class="{ delanimation: activeAnimation }" class="container__arrow"><i class="right"></i></p>
      </div>
      <div class="slider__dots dots">
      <div v-for="(dot, index) in images" :key="index" class="dots__dot" @click="slideClickChange(index)" v-bind:class="[{ active: currentItem === index }, { delanimation: activeAnimation }]">
      </div>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Slider',
  data () {
    return {
      images: ['image_1', 'image_2', 'image_3'],
      currentItem: 0,
      animateName: '',
      activeAnimation: null
    }
  },
  computed: {
    currentImage () {
      return require(`assets/${this.images[this.currentItem]}.jpg`)
    }
  },
  watch: {
    currentItem (newVal, oldVal) {
      if ((newVal === this.images.length - 1 && oldVal === 0)) {
        this.animateName = 'slideback'
      } else if (newVal > oldVal || (newVal === 0 && oldVal === this.images.length - 1)) {
        this.animateName = 'slidenext'
      } else {
        this.animateName = 'slideback'
      }
    },
    activeAnimation (newVal) {
      if (newVal) {
        setTimeout(() => {
          this.activeAnimation = false
        }, 1000)
      }
    }
  },
  methods: {
    goNext () {
      if (!this.activeAnimation) {
        this.activeAnimation = true
        if (this.currentItem < this.images.length - 1) {
          this.currentItem++
        } else {
          this.currentItem = 0
        }
      }
    },
    goBack () {
      if (!this.activeAnimation) {
        this.activeAnimation = true
        if (this.currentItem > 0) {
          this.currentItem--
        } else {
          this.currentItem = this.images.length - 1
        }
      }
    },
    slideClickChange (value) {
      if (!this.activeAnimation) {
        this.activeAnimation = true
        this.currentItem = value
      }
    },
    setTime (func) {
      setTimeout(func, 1000)
    }
  }
}

</script>

<style lang="scss" scoped>
.slider {
    background-color: silver;
}
.container {
        display: flex;
        flex-flow: row nowrap;
        justify-content: center;
        align-items: center;
        &__content {
            overflow: hidden;
            position: relative;
            width: 400px;
            height: 400px;
        }
         &__slide{
                position: absolute;
            }
        &__arrow {
            padding: 25px;
        }
    }
.dots {
    display: flex;
    flex-flow: row nowrap;
    justify-content: center;
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
.active {
          background-color: aliceblue;
        }
i {
  border: solid black;
  border-width: 0 10px 10px 0;
  display: inline-block;
  padding: 10px;
}
.delanimation {
pointer-events: none;
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

.slidenext-leave-active,
.slidenext-enter-active {
  transition: 1s;
}
.slidenext-enter {
  transform: translate(100%, 0);
}
.slidenext-leave-to {
  transform: translate(-100%, 0);
}

.slideback-leave-active,
.slideback-enter-active {
  transition: 1s;
}
.slideback-enter {
  transform: translateX(-100%);
}
.slideback-leave-to {
    transform: translateX(100%);
}
</style>
