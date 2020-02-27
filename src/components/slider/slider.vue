<template>
  <!-- SLIDER -->
  <div
    class="slider"
    ref="slider"
    @mousedown="mouseDown($event)"
    @mousemove="mouseMove($event)"
    @mouseup="mouseUp($event)"
  >
    <!-- SLIDER INNER -->
    <div class="slider__inner">
      <!-- SLIDE -->
      <slide
        v-for="(lm, index) in listMovies"
        :key="index"
        :id="index"
        :counter="counter"
        :slideImage="lm.image"
        :slideAltImage="lm.name"
        :slideBadgeTop="lm.badgeTop"
        :slideBadgeBottom="lm.badgeBottom"
        :slideName="lm.name"
        :slideTitle="lm.title"
      >
      </slide>
    </div>

    <!-- CONTROLLER -->
    <controller
      :listMovies="listMovies"
      :clickArrowLeft="actionLeft"
      :clickArrowRight="actionRight"
      :counter="counter"
      @changeCounter="counter = $event"
    />
  </div>
</template>

<script>
//
import slide from "@/components/slider/slide";
import controller from "@/components/slider/controller";

//
export default {
  name: "slider",
  props: {
    listMovies: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      counter: 0,
      startX: null,
      endX: null,
      statusEventDown: false,
      statusEventUp: false
    };
  },
  methods: {
    // FUNCTION RUNING WHENE CLICK ARROW RIGHT
    actionRight() {
      if (this.counter < this.listMovies.length - 1) {
        return this.counter++;
      }
    },

    // FUNCTION RUNING WHENE CLICK ARROW LEFT
    actionLeft() {
      if (this.counter > 0) {
        return this.counter--;
      }
    },

    //// ALL FUNCTION EVENT HANDELAR
    // VALIDATE SWIP
    validateSwip() {
      //
      const getWidthSlider = this.$refs.slider.clientWidth / 3;
      const scrolling = Math.abs(this.startX - this.endX);

      // CHECK IF SCROLLING LT WIDTH SLIDER WILL BR STOP FUNCTION AND RETURN FALSE
      if (scrolling < getWidthSlider) return false;

      // CHECK IF START X GT END X WILL BE RUNINNG FUNCTION ACTION RIGHT
      if (this.startX > this.endX) {
        // ACTION RIGHT
        this.actionRight();

        // IF START X LT END X WILL BE RUNINNG ACTION LEFT
      } else if (this.startX < this.endX) {
        // ACTION LEFT
        this.actionLeft();
      }
    },

    // MOUSE DOWN
    mouseDown(el) {
      // CHANGE STATUS TO TRUE
      this.statusEventDown = true;

      // CHANGE STATUS EVENT UP EQUAL FALSE
      this.statusEventUp = false;

      // SET PAGE X IN START X
      this.startX = el.pageX;
    },

    // MOUSE UP
    mouseUp(el) {
      // CHANGE STATUS TO FALSE
      this.statusEventDown = false;

      // IF STATUS EVENT UP TRUE WILL BE RUNING VALIDATE SWIP
      if (this.statusEventUp) this.validateSwip();
    },

    // MOUSE MOVE
    mouseMove(el) {
      // IF STATUS EVENT EQUAL FALSE WILL BE RETURN FALSE AND STOP RUNING THIS FUNCTION
      if (!this.statusEventDown) return;

      // SET PAGE X IN END X
      this.endX = el.pageX;

      // CHANGE STATUS EVENT UP EQUAL TRUE
      this.statusEventUp = true;
    }
  },
  components: {
    slide,
    controller
  }
};
</script>

<style></style>
