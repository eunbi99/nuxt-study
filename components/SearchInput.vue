<template>
    <div>
        <input 
            type="text" 
            :value="value" 
            @input="$emit('input', $event.target.value)"/> <!--input 태그에 걸려있는 value값들이 바뀔 때 마다 input 이벤트를 위로 올림-->
        <button type="button" @click="$emit('search')">search</button>
    </div>
</template>

<script>

export default({
    props: {
        value: {
            type: String,
            default: () => '',
        },
    },
})
</script>
