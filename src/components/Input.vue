<template>
    <div :class="[{inputUp: step === 1},'inputWrapper']">
        <h1 v-if="step === 0" class="input__title">Film Browser</h1>
        <input type="text" class="input"
        v-model="value"
         />
         <button class="input__button" v-on:click="handleClick">🔎</button>
    </div>
</template>
<script>
export default {
  name: 'Input',
  props: ['step'],
  data() {
    return {
      value: '',
    };
  },
  methods: {
    handleClick() {
      this.$emit('searchClick', this.value);
    },
  },
};
</script>
<style lang="scss" scoped>
    .inputWrapper{
        flex-basis: 100%;
        align-items: center;
        justify-content: center;
        display: flex;
        flex-wrap: wrap;
        margin: 10% 0 0 0;
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
        &:focus{
            box-shadow: 0 20px 10px -12px rgba(119, 119, 119, 0.829);
            // outline: none;
            // box-shadow: 0 12px 9px -10px black;
        }
        &__title{
        font-size: 100px;
        flex-basis: 100%;
        }
        &__button{
            cursor: pointer;
            margin: 30px 0 0 10px;
            padding: 5px 5px 15px 5px;
            border: 0;
            background-color: white;
            font-size: 30px;
            outline: none;
        }
    }
    .inputUp{
    margin: 20px 0 0 0;
    transition: margin-top 0.8s;
  }
</style>
