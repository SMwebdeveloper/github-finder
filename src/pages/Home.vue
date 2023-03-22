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
import axios from 'axios'
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
      axios.get(`https://api.github.com/users/${this.search}/repos`)
           .then(res => {
            console.log(res);
           }).catch(err => {
            console.log(err);
           })
    }
  }
}
</script>

<style lang="css">
.container{
    text-align: center;
}
</style>