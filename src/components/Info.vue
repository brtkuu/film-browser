<template>
    <div class="wrapper" v-if="item.poster_path !== null" v-on:click="dispMoreInfo">
        <div class="item_image">
        <img :src="photo" alt="">
        </div>
        <div class="item_title">
        <h2>{{ item.title }}</h2>
        <span class="item_date">Release date: {{ item.release_date }}</span>
        </div>
    </div>
</template>
<script>
export default {
  name: 'Info',
  props: ['item'],
  data() {
    return {
      photo: '',
    };
  },
  mounted() {
    this.photo = `https://image.tmdb.org/t/p/w185/${this.item.poster_path}`;
  },
  methods: {
    dispMoreInfo() {
      this.$emit('showInfo');
    },
  },
};
</script>
<style lang="scss" scoped>
.wrapper{
  cursor: pointer;
    display: flex;
    align-items: center;
    max-width: 1200px;
    flex-wrap: wrap;
    border-bottom: 1px solid black;
    border-top: 1px solid black;
    margin: 10px 0;
    justify-content: center;
    @media (max-width: 600px){
          justify-content: space-evenly;
        }
}
.item{
    &_image{
        margin: 5px 0 0 0;
        flex-basis: 45%;
    }
    &_title{
        font-size: 42px;
        text-align: left;
        flex-basis: 50%;
        @media (max-width: 600px){
          font-size: 20px;
          text-align: center;
        }
    }
    &_date{
        font-size: 20px;
        @media (max-width: 600px){
          font-size: 10px;
        }
    }
}
</style>
