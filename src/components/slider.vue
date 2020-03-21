<template>
  <section>
    <!-- Slideshow container -->
    <div class="slideshow-container">

      <!-- Full-width images with number and caption text -->
      <div class="mySlides fade" v-for="(photo,idx) in photos" :key="`photo${idx}`">
        <div v-show="showNumber" class="numbertext">{{idx+1}} / {{photos.length}}</div>
        <img :src="photo.src" class="w-100">
        <div class="text">{{photo.text}}</div>
      </div>
      <!-- Next and previous buttons -->
      <section v-for="(control, idx) in controls" :key="idx">
      <button-control 
        :type="control.prev" 
        @plus="plusSlides(control.number)"
      />
      </section>
    </div>
    <br>

    <!-- The dots/circles -->
    <div class="align-dots">
      <section v-for="(photo,idx) in photos" :key="`dot${idx}`">
      <span class="dot" @click="currentSlide(idx + 1)"></span>
      </section>
    </div>
  </section>
</template>

<script>
export default {
  name: 'slider',
  components: {
    'button-control': () =>  import('./buttons-controls.vue')
  },
  props: {
    showNumber: {
      type:Boolean,
      required:false,
      default:true
    },
    photos: {
      type:Array,
      required:false,
      default:() => [
        {
         text:1,
         src:"https://homepages.cae.wisc.edu/~ece533/images/airplane.png" 
        },
        {
         text:2,
         src:"https://i.ibb.co/JzVwm71/Add-Text-11-01-05-10-39.jpg"
        },
        {
         text:3,
         src:"https://homepages.cae.wisc.edu/~ece533/images/arctichare.png"
        },
        {
         text:4,
         src:"https://homepages.cae.wisc.edu/~ece533/images/cat.png"
        }
      ]
    }
  },
  data () {
    return {
      slideIndex: 1,
      element: '',
      index: 0,
      controls: [
      {
        prev:'prev',
        number: -1
      },
      {
        prev:'next',
        number: -1
      }
      ]
    }
  },
  mounted () {
    this.showSlides(this.slideIndex);
  },
  methods: {
    currentSlide (number) {
      this.showSlides(this.slideIndex = number);
      console.log(number)
    },
    plusSlides (number) {
      this.showSlides(this.slideIndex += number);
    },
    showSlides (number) {
      let slides = this.$el.getElementsByClassName("mySlides");
      let dots = this.$el.getElementsByClassName("dot");
      if (number > slides.length) { this.slideIndex = 1 }
      if (number < 1) { this.slideIndex = slides.length }
      for (this.i = 0; this.i < slides.length; this.i++) {
        slides[this.i].style.display = "none";
      }
      for (this.i = 0; this.i < dots.length; this.i++) {
        dots[this.i].className = dots[this.i].className.replace(" active", "");
      }
      slides[this.slideIndex - 1].style.display = "block";
      dots[this.slideIndex - 1].className += " active";
    }
  }
}
</script>

<style scoped>
* {
  box-sizing: border-box;
}
body {
  font-family: Verdana, sans-serif;
  margin: 0;
}
.mySlides {
  display: none;
}
img {
  vertical-align: middle;
}

/* Slideshow container */
.slideshow-container {
  max-width: 1000px;
  position: relative;
  margin: auto;
}

/* Hide the images by default */
.mySlides {
  display: none;
}

/* Caption text */
.text {
  color: #f2f2f2;
  font-size: 15px;
  padding: 8px 12px;
  position: absolute;
  bottom: 8px;
  width: 100%;
  text-align: center;
}

/* Number text (1/3 etc) */
.numbertext {
  color: #f2f2f2;
  font-size: 12px;
  padding: 8px 12px;
  position: absolute;
  top: 0;
}

/* The dots/bullets/indicators */
.dot {
  cursor: pointer;
  height: 15px;
  width: 15px;
  margin: 0 2px;
  background-color: #bbb;
  border-radius: 50%;
  display: inline-block;
  transition: background-color 0.6s ease;
}

.active,
.dot:hover {
  background-color: #717171;
}

/* Fading animation */
.fade {
  -webkit-animation-name: fade;
  -webkit-animation-duration: 1.5s;
  animation-name: fade;
  animation-duration: 1.5s;
}

@-webkit-keyframes fade {
  from {
    opacity: 0.4;
  }
  to {
    opacity: 1;
  }
}

@keyframes fade {
  from {
    opacity: 0.4;
  }
  to {
    opacity: 1;
  }
}
/* On smaller screens, decrease text size */
@media only screen and (max-width: 300px) {
  .prev,
  .next,
  .text {
    font-size: 11px;
  }
}
.align-dots {
  display:flex;
  justify-content: center
}
.w-100 {
  width: 100%;
}
</style>