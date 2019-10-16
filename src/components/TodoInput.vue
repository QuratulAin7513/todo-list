
<template lang="html">
<div class="col-sm-12">

<div class="row ">
<div class="col-sm-12">
  <div class="row">
    <div class="input-group">
     <i class="fas fa-plus fa-2x" style="padding-right:25px;color:rgb(130, 128, 122);"></i>
     <input type='text' class="inputfield" placeholder="Type your task..."  required v-on:keyup="show=true" v-on:keyup.enter="addTodo" v-model="text"/>
    <datetime class="dateborder" style="margin-right:0px;" format="YYYY-MM-DD h:i:s" v-model='dob' ></datetime>

      <button   v-if="show" type="button" class="btn btn-danger btn-sm"  v-on:click="addTodo">Add Task</button>
      
   </div>   </div>
</div>



      
            
 
</div>

</div>
</template>

<script>
import datetime from 'vuejs-datetimepicker'
var moment = require("moment");
moment().format();
export default {
  components: { datetime },
  methods: {
    
    addTodo() {
      if(this.text.trim().length===0)
      {
        return
      }
  
      else{

      
      this.$emit("todo:add", this.text,this.dob);
      this.text = "";
      }
    },
    
  },
  name: "todo-input",
  data() {
    return {
      text: "",
      dob:moment(),
      show: false,
      currentTime:moment()
    };
  },
  
};
</script>
<style type="css">
.todo-input-wrapper {
  margin-bottom: 20px;
}

input:focus{
  border:none;
}

.inputfield {
  width:100%;
  border:none;

  border-right:solid 2px rgb(189, 185, 185);
  padding-right: 80px;
   }
.dateborder input {
  border:none;
  width:100%;
   padding:20px;
}




 
</style>
