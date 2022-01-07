<template>
  <div class="restaurant--card">
    <div :style="changeBackground" class="restaurant--image"></div>
    <div class="restaurant--info">
      <div class="top">
        <p class="name">{{ info_restau.name}}
        </p>
        <p class="note">
          <span>{{ info_restau.note }}</span> </p>
      </div>
      <p class="time">{{ info_restau.drive_time}}</p>
    </div>
  </div>
</template>

<script>
// import
import { computed } from 'vue'
export default {
  name: "RestaurantCard",
  props: {
    info_restau: Object
  },
  setup(props) {
    //console.log(props.info_restau)
    const changeBackground = computed(() => {
      return {
        backgroundImage: `url(${props.info_restau.image})`
      }
    }
  )
    
  return {
    changeBackground
    }
  }
}
</script>

<style lang="scss">
.restaurant--card {
  width: 32%;
  height: 30vh;
  .restaurant--image {
    background-image: url("./../../public/img/class menu 1250.png");
    height: 70%;
  }
  // top dans restau-info
  .restaurant--info {
    .top {
    margin: 10px 0px;
      display: flex;
      align-items: center; //aligner les elts enfants ici name et note
      justify-content: space-between; // repoousse aux extremités jcsb
      // style la note, span dans la note car note suivant état, et dans rond gris
      .note {
        background-color: #eeeeee; // bgc#eee bg gris
        height: 30px;
        width: 30px;
        display: flex;
        justify-content: center; //jcc
        align-items: center; //aic
        font-size: 0.8rem;
        border-radius: 50%;
      }
    }
    .time {
        font-style: 0.9rem; //fz0.9
    }
  }
}

</style>