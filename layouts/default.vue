<template>
    <div>
        <header>
            <h1>{{$route.name}}페이지</h1>
            <Nuxt-link to="/"> 홈페이지 </Nuxt-link>
            <Nuxt-link to="/main">메인페이지</Nuxt-link>
            <Nuxt-link to="/product">상품페이지</Nuxt-link>
        </header>
        <Nuxt />
    </div>
</template>

<script>

export default {
    // created(){
    //     console.log(this.$route)
    // }
}
</script>

