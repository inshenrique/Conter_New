<template>
  <div class="split-flap-container">
    <div v-for="(digit, index) in displayDigits" :key="index" class="split-flap">
      <span>{{ digit }}</span>
    </div>
  </div>
</template>

<script>
import gsap from "gsap";

export default {
  props: {
    number: {
      type: Number,
      required: true
    }
  },
  data() {
    return {
      displayDigits: Array(6).fill(0),
      previousNumber: 0
    };
  },
  watch: {
    number(newVal) {
      this.animateFlap(newVal);
    }
  },
  methods: {
    animateFlap(newNumber) {
      const newDigits = newNumber.toString().padStart(6, "0").split("");
      newDigits.forEach((digit, index) => {
        if (this.displayDigits[index] !== digit) {
          gsap.to(this.$el.children[index], {
            duration: 0.5,
            y: -10,
            opacity: 0,
            onComplete: () => {
              this.displayDigits[index] = digit;
              gsap.fromTo(
                this.$el.children[index],
                { y: 10, opacity: 0 },
                { duration: 0.5, y: 0, opacity: 1 }
              );
            }
          });
        }
      });
    }
  },
  mounted() {
    this.animateFlap(this.number);
  }
};
</script>

<style>
.split-flap-container {
  display: flex;
  font-size: 2rem;
  font-weight: bold;
  font-family: monospace;
}

.split-flap {
  display: inline-block;
  width: 40px;
  height: 60px;
  background: black;
  color: white;
  text-align: center;
  font-size: 2rem;
  font-weight: bold;
  line-height: 2rem;
  border-radius: 4px;
  margin: 0 2px;
  overflow: hidden;
  position: relative;
  display: inline-block;
  text-align: center;
}
</style>