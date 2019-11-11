<template>
  <div class="text-center">
    <!-- 입력을 입력할때마다 결과가 변한다. -->
    <!-- <input type="text" v-on:input="onInput"> -->
    <!-- api 횟수가 제한되므로, 일단 enter를 치면 결과가 나오도록 설정한다. -->
    <input class="w-75" type="text" v-on:keydown.enter="onInput">
  </div>
</template>

<script>
export default {
  name: 'SearchBar',
  // 이름이 onInput인 함수를 만들어준다.
  methods: {
    onInput(e){
      // console.log(e)
      // $emit(event를 어떻게 부를지, App으로 보낼 사용자가 입력한 데이터)
      // emit은 한단계 위의 부모에게만 보낼 수 있다. 
      // 자식 컴포넌트와 부모 컴포넌트의 이름은 다를 수 있다.
      // 부모 - App.vue
      this.$emit('inputChange', e.target.value)
    }
  }
}
</script>

<style>

</style>