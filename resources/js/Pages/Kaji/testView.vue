<template>
    <div class="todolistContainer">
        <div class="heading">
            <h2 id="title">Opportunites</h2>
            <h2 id="title">Merci a notre partenaire <strong class="senga">www.senga-service.com</strong></h2>
            <h2 id="title">Opportunites par des companies, click <inertia-link  class="senga" href="/c/o">ici.</inertia-link></h2>
        </div>
        
        <div class="row">
                <div>
                    <input v-model="term" @keyup="search"  name="" id="" type="text" placeholder="Recherche" required class="ring ring-gray-300 w-full rounded-md px-4 py-2 outline-none focus:ring-2 focus:ring-teal-300">
                </div>
        </div>

        <test-list :items="searchItems"
        v-on:reloadlist="getList()"/>

    </div>
</template>

<script>
import PartList from './partList.vue'
import TestList from './testList.vue'
import _ from 'lodash'

    export default {

        props:['searchItems'],

        components:{

                PartList,
                TestList
        },
        data: function () {
            return{
                term:''
            }
        },
        methods: {
            getList () {
                axios.get('/api/p').then(response => {
                    this.searchItems =response.data
                }).catch(error => {
                    console.log(error);
                })
            },
            search: _.throttle(function(){
                this.$inertia.replace(this.route('test',{term:this.term}))
            }, 200),
            
        },
        created(){
            this.getList();
        }

    }
</script>

<style scoped>
.todolistContainer{
    width: 350;
    margin: auto;
}
.heading{
    background: #e6e6e6;
    padding: 10px;
}
#title{
    text-align: center;
}
.senga{
    color: blue;
}
</style>