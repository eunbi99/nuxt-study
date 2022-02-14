<template>
        <div class="app">
          <main>
            <!--
              :search-keyword='searchKeyword'
              @input="updateSearchKeyword"
              대신 v-model을 사용함으로서, 메소드를 하나 줄일 수 있다.
              단점: v-model은 한국어 입력을 다룰 때ㅡ 한 글자에 대한 입력이 끝나야지만 동기화가 되기 때문에 한계점이 있다.
            -->
            <SearchInput
              v-model="searchKeyword"
              @search="searchProducts"
            />
            <ul>
                <li v-for="product in products" :key="product.id" class="item flex" @click="moveToDetailPage(product.id)">
                    <img class="product-image" :src="product.imageUrl" :alt="product.name" />
                    <p>{{product.name}}</p>
                    <span>{{product.price}}</span>
                </li>
            </ul>
          </main>
        </div>
</template>

<script>
import axios from 'axios'
import { fetchProductsByKeyword } from "../api";
import SearchInput from '@/components/SearchInput.vue'

export default {
      components: { SearchInput },
      async asyncData(){
        const response = await axios.get('http://localhost:3000/products')

        /* eslint-disable no-console */
        console.log(response)
        /* eslint-enable no-console */
        const products = response.data.map((item) =>({
          ...item,
          imageUrl:`${item.imageUrl}?random=${Math.random()}`,
        }))
        return { products }
  },
  data() {
    return {
      searchKeyword: '',
    }
  },
  methods:{
    moveToDetailPage(id) {
      this.$router.push(`detail/${id}`)
    },
    async searchProducts() {
      const response = await fetchProductsByKeyword(this.searchKeyword);
      console.log(response);
      this.products = response.data.map((item) =>({
        ...item,
        imageUrl:`${item.imageUrl}?random=${Math.random()}`,
      }))
    }
  }
//   data(){
//       return {
//           products: [],
//       }
//   },

//   async created(){},
}
</script>

<style scoped>
.flex {
  display: flex;
  justify-content: center;
}
.item {
  display: inline-block;
  width: 400px;
  height: 300px;
  text-align: center;
  margin: 0 0.5rem;
  cursor: pointer;
}
.product-image {
  width: 400px;
  height: 250px;
}
.app {
  position: relative;
}
.cart-wrapper {
  position: sticky;
  float: right;
  bottom: 50px;
  right: 50px;
}
.cart-wrapper .btn {
  display: inline-block;
  height: 40px;
  font-size: 1rem;
  font-weight: 500;
}
</style>
