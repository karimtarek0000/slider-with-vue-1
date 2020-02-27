<template>
  <div class="home">
    <slider :listMovies="listMoviesSlider" />
  </div>
</template>

<script>
// ALL IMPORTANT
import slider from "@/components/slider/slider";

export default {
  name: "Home",
  data() {
    return {
      listMoviesSlider: [
        {
          name: "avangers end game",
          title: "coming soon on netflix",
          badgeTop: "movies",
          image: "https://i.imgur.com/RaODibw.png"
        },
        {
          name: "the irshmen",
          title: "coming soon on netflix",
          badgeTop: "movies",
          image: "https://i.imgur.com/S1BBFX0.jpg"
        },
        {
          name: "la casa de papel",
          title: "coming soon on netflix",
          badgeTop: "series",
          badgeBottom: "season 3",
          image: "https://i.imgur.com/3MNg8r3.jpg"
        },
        {
          name: "the age of adaline",
          title: "coming soon on netflix",
          badgeTop: "movies",
          image: "https://i.imgur.com/NaJvE4L.jpg"
        }
      ]
    };
  },
  components: {
    slider
  }
};
</script>

<style></style>
