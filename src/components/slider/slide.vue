<template>
  <transition @enter="enterAnim" @leave="leaveAnim">
    <!-- SLIDE -->
    <div class="slider__slide" v-show="show">
      <!-- IMAGE -->
      <img :src="slideImage" :alt="slideAltImage" />

      <!-- SLIDER CONTENT -->
      <div class="slider__overlay">
        <div class="slider__content">
          <span class="slider__badgeTop">{{ slideBadgeTop }}</span>
          <h2 class="slider__name">{{ slideName }}</h2>
          <p class="slider__title">{{ slideTitle }}</p>
          <span class="slider__badgeBottom" v-if="slideBadgeBottom">{{
            slideBadgeBottom
          }}</span>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "slide",
  props: {
    id: {
      type: Number,
      required: true,
      default: 0
    },
    counter: {
      type: Number,
      required: true,
      default: 0
    },
    slideImage: {
      type: String,
      required: true
    },
    slideAltImage: {
      type: [String, Number],
      required: false
    },
    slideBadgeTop: {
      type: String,
      required: true
    },
    slideBadgeBottom: {
      type: String,
      required: false
    },
    slideName: {
      type: String,
      required: true
    },
    slideTitle: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      duration: 1,
      fromEnter: null,
      toEnter: null,
      fromLeave: null,
      toLeave: null
    };
  },
  methods: {
    // ENTER ANIM
    enterAnim(el, done) {
      //
      const elSlider = el,
        elOverlay = el.querySelector(".slider__overlay"),
        elContent = el.querySelector(".slider__content"),
        tl = new TimelineMax({ delay: this.duration });

      // TRACK ANIMATION
      tl.fromTo(
        elSlider,
        this.duration,
        { xPercent: this.fromEnter },
        { xPercent: this.toEnter, ease: Power1.easeInOut }
      )
        .fromTo(
          elOverlay,
          this.duration,
          { autoAlpha: 0, xPercent: this.fromEnter },
          { autoAlpha: 1, xPercent: this.toEnter, ease: Power1.easeInOut },
          "-=0.5"
        )
        .fromTo(
          elContent,
          this.duration,
          { autoAlpha: 0, xPercent: this.fromEnter },
          { autoAlpha: 1, xPercent: this.toEnter, ease: Power1.easeInOut },
          "-=0.5"
        );
    },

    // LEAVE ANIM
    leaveAnim(el, done) {
      //
      const elSlider = el,
        elOverlay = el.querySelector(".slider__overlay"),
        elContent = el.querySelector(".slider__content"),
        tl = new TimelineMax();

      // TRACK ANIMATION
      tl.to(elContent, this.duration, {
        autoAlpha: 0,
        xPercent: this.toLeave,
        ease: Power1.easeInOut
      })
        .to(
          elOverlay,
          this.duration,
          { autoAlpha: 0, xPercent: this.toLeave, ease: Power1.easeInOut },
          "-=0.5"
        )
        .fromTo(
          elSlider,
          this.duration,
          { xPercent: this.fromLeave },
          { xPercent: this.toLeave, ease: Power1.easeInOut },
          "-=0.5"
        );
    }
  },
  computed: {
    // SHOW
    show() {
      return this.id == this.counter;
    }
  },
  watch: {
    // WATCH COUNTER CLICKS AND WILL BE CHANGE TRACK ANIMATION
    counter(newCount, oldCount) {
      if (newCount > oldCount) {
        this.fromEnter = 100;
        this.toEnter = 0;
        this.fromLeave = 0;
        this.toLeave = -100;
      } else {
        this.fromEnter = -100;
        this.toEnter = 0;
        this.fromLeave = 0;
        this.toLeave = 100;
      }
    }
  }
};
</script>

<style></style>
