<template>
    <div>
        <input
          type="text"
          :value="value"
          @input="$emit('input',$event.target.value)" />
        <button type="button" @click="$emit('search')">search</button>
    </div>
</template>

<script>

export default({
  // 상위 컴포넌트인 index.vue에서 v-model로 값을 내려주면 props에서 value로 받아 searchInput.vue의 value로 값이 들어간다!
  props: {
    value: {
      type:String,
      default: () => '',
    }
  }

})
</script>
