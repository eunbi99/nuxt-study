<template>
    <div>
        {{ products }}
    </div>
</template>

<script>
import axios from 'axios'
export default {
    async asyncData(){
        const response = await axios.get('http://localhost:3000/products')
        /* eslint-disable no-console */
        console.log(response)
        /* eslint-enable no-console */
        const products = response.data
        return { products } 
  },
}
</script>
