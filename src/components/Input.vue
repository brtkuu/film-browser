<template>
  <div>
    <div :class="[{inputUp: step === 1},'inputWrapper']">
        <h1 v-show="step === 0" class="input__title">Film Browser</h1>
        <input type="text" class="input"
        v-model="value"
        v-on:keyup.enter="handleClick"
         />
         <button class="input__button" v-on:click="handleClick">
           🔎
         </button>
        <select class="input__select" @change="handleChange($event)"  v-show="step === 1">
          <option value="title" selected>Sort by name</option>
          <option value="popularity">Sort by popularity</option>
        </select>
    </div>
  </div>
</template>
<script>
export default {
  name: 'Input',
  props: ['step'],
  data() {
    return {
      value: '',
      filter: '',
    };
  },
  methods: {
    handleClick() {
      this.$emit('searchClick', { searchValue: this.value, filter: this.filter });
    },
    handleChange(event) {
      this.filter = event.target.value;
      this.$emit('searchClick', { searchValue: this.value, filter: this.filter });
    },
  },
};
</script>
<style lang="scss" scoped>
    .inputWrapper{
        flex-basis: 100%;
        width: 100vw;
        align-items: center;
        justify-content: center;
        display: flex;
        flex-wrap: wrap;
        margin: 10% 0 0 0;
        @media (max-width: 950px) {
        margin-top: 50%;
    }
    }
    .input{
        background: none;
        width: 250px;
        text-align: center;
        font-size: 40px;
        border: 0;
        border-bottom: 2px solid black;
        transition: box-shadow 0.2s;
        outline: none;
        &__select{
          font-size: 24px;
          margin: 5px;
          background: none;
          border: none;
          border-bottom: 2px solid;
        }
        &:focus{
            box-shadow: 0 20px 10px -12px rgba(119, 119, 119, 0.829);
            // outline: none;
            // box-shadow: 0 12px 9px -10px black;
        @media (max-width: 600px) {
            box-shadow: 0 20px 10px -12px rgba(255, 255, 255, 0.829);
        }
        }
        &__title{
        font-size: 100px;
        flex-basis: 100%;
        @media (max-width: 950px) {
        font-size: 70px;
        }
        @media (max-width: 600px) {
        color: white;
        }
        }
        &__button{
            cursor: pointer;
            margin: 30px 0 0 10px;
            padding: 5px 5px 15px 5px;
            border: 0;
            background-color: rgba(0,0,0,0);
            font-size: 30px;
            outline: none;
          @media (max-width: 600px) {
            display: none;
          }
        }
    }
    .inputUp{
    margin: 20px 0 0 0;
    transition: margin-top 0.8s;
  }
</style>
