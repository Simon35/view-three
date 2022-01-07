<template>
  <div class="home">
    <div class="header">
      <img src="../../public/img/emoji2.png" alt="" srcset="">
      <div class="wrapper--input">
        <input v-model="user_search_restau" type="text" placeholder="De quoi avez-vous envie ?">

        <div class="search">
          <div v-for="(restau, i) in search_rest" :key="i" class="container--rest--search">
            <div class="wrapper--img">
              <img :src="restau.image" alt="" srcset="">
            </div>
            <h2>{{ restau.name }}</h2>
          </div>
        </div>

      </div>
    </div>
    <RestaurantRow v-for="(data, i) in dataRestau" :key="i" :three_restau="data"/>
  </div>
</template>

<script>
//IMPORT
import BDD from '../BDD.js'
import {onMounted, ref, watch} from 'vue'
// Components
import RestaurantRow from '../components/RestaurantRow.vue'
export default {
  name: 'Home',
  components: {
    RestaurantRow
  },
  setup() {
    class Restaurant {
      constructor(name, note, image, drive_time){
        this.name = name
        this.note = note
        this.image = image
        this.drive_time = drive_time
      }
    }

    let dataRestau = ref([]);
    let all_restau = [];

    const makeDataRestau = () => {
      let three_restau = [];

      for(const restau of BDD) {
        const new_restau = new Restaurant(restau.name, restau.note, restau.image, restau.drive_time)
        //console.log(restau);
        // make all restau array
        all_restau.push(new_restau);

        if(three_restau.length === 2){
          three_restau.push(new_restau);
          dataRestau.value.push(three_restau);
          three_restau = [];
        }else {
          three_restau.push(new_restau);

        }
      }
        console.log(dataRestau);

    }

    // user search restau
    let user_search_restau = ref('');
        let search_rest = ref('');

    watch(user_search_restau, new_value => {
      //console.log(new_value, all_restau)
      let regex = RegExp(new_value.toLowerCase());
      let new_search_rest = all_restau.filter(restau => regex.test(restau.name.toLowerCase()));
      //console.log(search_rest);
      search_rest.value = new_search_rest;

      if(new_value == 0) {
        search_rest.value = []
        
      } else {
        search_rest.value = new_search_rest;
      }
      
    })

    onMounted(makeDataRestau);

    return {
      dataRestau,
      user_search_restau,
      search_rest  
    }

    //var resto = new Restaurant('toto',4,5, 'img','45 min')
    //console.log(resto)
    //console.log(BDD)
  }

}

</script>

<style lang="scss" scoped>
.home {
  .header {
    height: 120px;
    width: 100%;
    display: flex;
    align-items: center;
    justify-content: space-between;
    img {
      width: 100px;
    }
    .wrapper--input{
      position: relative;

      input {
        background-color: #f6f6f6;
        border: none;
        height: 60px;
        width: 400px;
        outline: none;
        padding-left: 20px;
      }
      .search{
        position:absolute;
        top:100%;
        width:100%;
        background-color:#fff;

        .container--rest--search{
          display: flex;
          align-items: center;
          padding: 10px;

          .wrapper--img{
            height: 60px;
            width: 60px;
            margin-right: 25px;
            border-radius: 50%;
            overflow: hidden;

            img{
              height: 100%;
              width: auto;
            }
          }
        }
      }
    }
  }
}
</style>