<template>
  <section class="slider">
    <img class="slider__ship" src="../assets/shipnolight.svg" alt="ship" />
    <div class="slider__prev">
      <img
        v-if="value < 0"
        @click="move(100 / 3)"
        src="../assets/arrow-left.svg"
        alt="left"
      />
    </div>
    <div class="slider__container">
      <div ref="modals" class="slider__modals">
        <div class="slide">
          <Modall class="slide" :fishData="fishData" />
        </div>
        <div class="slide">
          <Video class="slide" :fishData="fishData" />
        </div>
        <div class="slide">
          <Map class="slide" :link="fishData.link" />
        </div>
      </div>
    </div>
    <div class="slider__next">
      <img
        v-if="value > -65"
        @click="move(-(100 / 3))"
        src="../assets/arrow-right.svg"
        alt="right"
      />
    </div>
    <img class="slider__seaweed" src="../assets/seaweed.svg" alt="seaweed" />
    <img
      class="slider__close"
      @click="$emit('close')"
      src="../assets/closepopup.svg"
      alt="close"
    />
  </section>
</template>

<script>
import Video from "@/components/Video.vue";
import Map from "@/components/Map.vue";
import Modall from "@/components/Modall.vue";

export default {
  name: "SliderModal",
  components: {
    Video,
    Map,
    Modall,
  },
  props: {
    fishData: Object,
  },
  data() {
    return {
      value: 0,
    };
  },
  methods: {
    move: function(value) {
      this.addToValue(value);
      this.$refs.modals.style.transform = `translateX(${this.value}%)`;
    },
    addToValue: function(distance) {
      this.value += distance;
    },
  },
};
</script>

<style scoped lang="scss">
.slider {
  position: fixed;
  display: flex;
  justify-content: space-between;
  align-items: center;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #4db2ce;
  width: 80%;
  height: 80%;
  border: 4px #fefcd0 solid;
  padding: 20px;
  border-radius: 10px;
}

.slider__ship {
  position: fixed;
  top: 0;
  left: 0;
  transform: translate(-50%, -50%);
}

.slider__seaweed {
  position: fixed;
  bottom: 0;
  right: 10px;
}

.slider__close {
  cursor: pointer;
  position: fixed;
  top: 20px;
  right: 20px;
}

.slider__container {
  overflow: hidden;
  width: 80%;
  height: 80%;
}

.slider__modals {
  display: flex;
  overflow: hidden;
  width: 300%;
  height: 100%;
}

.slide {
  width: 100%;
  height: 100%;
}

@media (max-width: 768px) {
  .slider__prev,
  .slider__next {
    display: none;
  }
  .slider__seaweed {
    position: fixed;
    width: 60px;
    bottom: 0;
    right: 10px;
  }
  .slider__ship {
    position: fixed;
    width: 100px;
    height: 100px;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);
  }
  .slider__container {
    width: 90%;
    height: 90%;
  }
  .slider__modals {
    display: flex;
    flex-direction: column;
    width: 100%;
    height: 120%;
    overflow-y: auto;
    :nth-child(1) {
      width: 100%;
      height: 100%;
    }
    :nth-child(2) {
      width: 100%;
      height: 100%;
    }
    :nth-child(3) {
      width: 100%;
      height: 100%;
    }
  }
}

@media screen and (min-width: 320px) and (max-width: 425px) {
  .slider__ship {
    position: fixed;
    width: 50px;
    height: 50px;
    top: 0;
    left: 0;
    transform: translate(-50%, -50%);
  }
  .slider__seaweed {
    position: fixed;
    width: 40px;
    bottom: 0;
    right: 10px;
  }
  .slider__modals {
    :nth-child(2) {
      width: 100%;
      height: 40%;
    }
    :nth-child(3) {
      width: 70%;
      height: 100%;
    }
  }
}
</style>
