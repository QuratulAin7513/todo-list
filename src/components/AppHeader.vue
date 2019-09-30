<template lang="html">
<div class="col-sm-12">
    <div class="row">
        <div class="col-sm-12 mt-4 mb-4">
            <div class="d-flex  justify-content-between w-100 m-1 text-primary">
            <h1>{{currentTime.format('dddd, Do')}}</h1>
            <p class="month mt-2">{{nextId}} Tasks </p>
            
            </div>
            <div class="d-flex  justify-content-between w-100 m-1 text-primary">
            <h3 class="month">{{currentTime.format('MMMM')}}</h3>
           <button v-if="displayBtn" type="button" class="btn btn-danger btn-sm" v-on:click="clearList">CLEAR LIST</button>
            
            </div> 
     
     </div>
    </div>
</div>


</template>

<script>
var moment = require("moment");
moment().format();
export default {
    name:'app-header',
     
     props: ["nextId","displayBtn"],
    data(){
        return{
        currentTime:moment()
        }
    },
    methods:
    {
        clearList()
        {
            this.$emit("clear:list");
        }
    }
   
    }


</script>
<style type="css">
.month{
    color:rgb(130, 128, 122);
}

</style>
