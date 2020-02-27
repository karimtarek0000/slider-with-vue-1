<template>
  <!-- SLIDER CONTROLLER -->
  <div class="slider__controller">
    <!-- ARROW -->
    <div class="slider__arrow">
      <svg
        ref="arrowLeft"
        class="slider__arrow__left"
        :style="{ opacity: changeColorArrowLeft }"
        @click="clickArrowLeft"
        xmlns="http://www.w3.org/2000/svg"
        width="13.967"
        height="23.953"
      >
        <path
          d="M-.005 11.976a.828.828 0 00.24.551l11.189 11.186a.754.754 0 001.1 0l1.2-1.2a.781.781 0 00.24-.551.828.828 0 00-.24-.551s-8.686-5.93-8.686-9.435 8.689-9.434 8.689-9.434a.754.754 0 000-1.1l-1.2-1.2a.754.754 0 00-1.1 0L.24 11.425a.824.824 0 00-.245.551z"
          fill="#fff"
        />
      </svg>
      <svg
        class="slider__arrow__right"
        :style="{ opacity: changeColorArrowRight }"
        @click="clickArrowRight"
        xmlns="http://www.w3.org/2000/svg"
        width="13.967"
        height="23.953"
      >
        <path
          d="M13.967 11.976a.828.828 0 01-.24.551L2.542 23.713a.824.824 0 01-.552.24.828.828 0 01-.552-.24l-1.2-1.2a.781.781 0 01-.24-.551.828.828 0 01.24-.551s8.69-5.929 8.69-9.434S.24 2.542.24 2.542a.754.754 0 010-1.1l1.2-1.2a.824.824 0 01.555-.246.828.828 0 01.552.24l11.181 11.189a.824.824 0 01.239.551z"
          fill="#fff"
        />
      </svg>
    </div>
    <!-- INDECATORS -->
    <ul class="slider__indecators" ref="indecators">
      <li
        class="slider__indecators__item"
        v-for="(indecators, index) in countIndecators"
        :key="index"
        @click="clickIndecator($event, index)"
      ></li>
      <li
        class="slider__indecators__item slider__indecators__item--move"
        ref="indecatorMove"
      ></li>
    </ul>
  </div>
</template>

<script>
export default {
  name: "controller",
  props: {
    listMovies: {
      type: Array,
      required: true
    },
    counter: {
      type: Number,
      required: true
    },
    clickArrowRight: Function,
    clickArrowLeft: Function
  },
  data() {
    return {
      maxIndecators: 7
    };
  },
  computed: {
    // GET COUNT SLIDES AND SET COUNT INDECATORS
    countIndecators() {
      return this.listMovies.length <= this.maxIndecators
        ? this.listMovies.length
        : this.maxIndecators;
    },
    // CHANGE STYLE ARROW CONTROLLER
    changeColorArrowLeft() {
      return this.counter == 0 ? 0.5 : 1;
    },
    changeColorArrowRight() {
      return this.counter == this.listMovies.length - 1 ? 0.5 : 1;
    }
  },
  methods: {
    // WHENE CLICK INDECATORS WILL BE GET INDEX AND CHANGE LEFT ELEMENT MOVE
    clickIndecator(el, index) {
      // REFS INDECATORS MOVE
      const elementMove = this.$refs.indecatorMove;

      // CHANGE LEFT POSITION WITH INDEX INDECATORS WHENE CLICK
      elementMove.style.left = el.toElement.offsetLeft + "px";

      // CUSTOM EVENT KNOW OTHER COMPONENT CHANGES DATA
      this.$emit("changeCounter", index);
    }
  },
  watch: {
    // WHENE CLICK ARROW WILL BE CLICK INDECATORS AND RUNINNG FUNCTION
    counter(newCount) {
      this.$refs.indecators.children[newCount].click();
    }
  }
};
</script>

<style></style>
