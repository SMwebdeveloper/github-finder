<template lang="">
    <div class="wrapper-content wrapper-content--fixed home">
        <section>
            <div class="container">
                <search :value="search" placeholder="Type username..." @search="search = $event"/>
                <button class="btn-primary" @click="getRepos">Search!</button>
            </div>
        </section>
    </div>
</template>
<script>
import search from '@/components/Search.vue';
export default {
  components:{
    search
  },
  data () {
    return{
        search: ''
    }
  },
  methods:{
    getRepos () {
        console.log(`get user ${this.search} repos`);
    }
  }
}
</script>

<style lang="css">
.container{
    text-align: center;
}
</style>