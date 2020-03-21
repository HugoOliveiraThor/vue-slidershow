<template>
<section>
  <a v-if="type == 'prev'" class="prev" @click="action()">&#10094;</a>
  <a v-if="type === 'next'" class="next" @click="action()">&#10095;</a>
</section>
</template>

<script>
export default {
  name: "button-control",
  props: {
    icon: {
      type:String,
      required:false,
      default:''
    },
    type: {
      type:String,
      required:false,
      default:''
    }
  },
  methods: {
    action() {
      this.$emit("plus");
    }
  }
};
</script>

<style lang="scss" scoped>
/* Next & previous buttons */
.prev,
.next {
  cursor: pointer;
  position: absolute;
  top: 50%;
  width: auto;
  margin-top: -22px;
  padding: 16px;
  color: white;
  font-weight: bold;
  font-size: 18px;
  transition: 0.6s ease;
  border-radius: 0 3px 3px 0;
  user-select: none;
}

/* Position the "next button" to the right */
.next {
  right: 0;
  border-radius: 3px 0 0 3px;
}
.prev {
  left: 0;
  border-radius: 3px 0 0 3px;
}
/* On hover, add a black background color with a little bit see-through */
.prev:hover,
.next:hover {
  background-color: rgba(0, 0, 0, 0.8);
}
</style>
