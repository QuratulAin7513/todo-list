<template lang="html">
<div class="col-sm-12">
  <div class=" d-flex  justify-content-between">
      <div class="row m-4 ">  
       <div class="col ">

         
            <div class="row d-flex">
             
                <label class="checkbox ">
                   <input type="checkbox" checked="checked" class="form-check-input mr-20" :id="todo.id"  :checked="todo.status==='complete'" v-on:change="changeStatus" value="">
                   <span class="checkmark"></span>
                </label>
             
              
           <div> 
           <div v-if="todo.status==='complete'" style=" text-decoration: line-through;">
             <div class="todo-item-left">
               <div v-if="!todo.editing" class="todo-item-label" @click="editTodo(todo)">
                 {{todo.text}}
               </div>
               <input v-else type="text" class="todo-item-edit" v-model="todo.text" @blur="doneEdit(todo)" @keyup.Enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus/>
             </div>
             
           </div>
           <div class="todo-item-left" v-else>
            <div v-if="!todo.editing" class="todo-item-label" @click="editTodo(todo)">
              {{todo.text}}
            </div>
            <input  v-else type="text" class="todo-item-edit" v-model="todo.text" @blur="doneEdit(todo)" @keyup.Enter="doneEdit(todo)" @keyup.esc="cancelEdit(todo)" v-focus/>
           
         
      </div>
      </div>


          
      </div>
     
           
  </div>
</div>
   
    
    
     <div class="row m-4 d-flex align-item-center text-muted">
            
       
        <div v-if="todo.duedate != null">
          {{todo.duedate.fromNow()}}
         <template v-if="compareTime(index)">/ OverDue</template>
         </div>
         <div class="remove-item" @click="removeTodo(index)">
           &times;
         </div>
      
    
    </div>  
   
      
  </div>
</div>
</template>

<script>
export default {
  name: "todo-item",
  props: ["todo", "compareTime", "index"],
  data(){
    return{
      visible:true
    };
  },
  directives: {
  focus: {
    
    inserted: function (el) {
      el.focus()
    }
  }
},
 
  methods: {
    changeStatus() {
      this.$emit("change:status");
    },
    removeTodo(index)
    {
      this.$emit("todo:remove",index);
    },
    editTodo(todo)
    {
      this.$emit("todo:edit",todo);
    },
    doneEdit(todo)
    {
      this.$emit("edit:done",todo);
    },
    cancelEdit(todo)
    {
      this.$emit("edit:cancel",todo);
    }
  }
};
</script>
<style type="css">
.smalltime {
  display: inline-block;
  border-bottom: 1px dotted black;
}

.smalltime .largetime {
  visibility: hidden;
  width: 220px;
  background-color: black;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 5px 0;

  /* Position the tooltip */
  position: absolute;
  z-index: 1;

  left: 63%;
  margin-left: -60px;
}
.active {
  border: 2px solid;
  border-color: red;
  padding: 2px;
}

.smalltime:hover .largetime {
  visibility: visible;
}
.checkbox {
  display: block;
  position: relative;
  padding-left:40px;
  margin-right:20px;
  margin-bottom: 12px;
  cursor: pointer;
  font-size:default;
 
  user-select: none;
}

/* Hide the browser's default checkbox */
.checkbox input {
  position: absolute;
  opacity: 0;
  cursor: pointer;
  height: 0;
  width: 0;
}

/* Create a custom checkbox */
.checkmark {
  position: absolute;
  top: 0;
  left: 0;
  height: 25px;
  width: 25px;
  background-color:white;
 
}

/* On mouse-over, add a grey background color */
.checkbox:hover input ~ .checkmark {
  background-color: #ccc;
}

/* When the checkbox is checked, add a blue background */
.checkbox input:checked ~ .checkmark {
  background-color: rgba(243, 33, 51, 0.753);
}

/* Create the checkmark/indicator (hidden when not checked) */
.checkmark:after {
  content: "";
  position: absolute;
  display: none;
}

/* Show the checkmark when checked */
.checkbox input:checked ~ .checkmark:after {
  display: block;
}

/* Style the checkmark/indicator */
.checkbox .checkmark:after {
  left: 9px;
  top: 5px;
  width: 5px;
  height: 10px;
  border: solid white;
  border-width: 0 3px 3px 0;
  -webkit-transform: rotate(45deg);
  -ms-transform: rotate(45deg);
  transform: rotate(45deg);
}
.remove-item{
  cursor: pointer;
  margin-left: 30px;
  font-size: 25px;
 
   
  
}
.remove-item:hover{
  color:black;
}
.todo-item-edit{
 
  color:#2c3e50;
  margin-left:-10px;
  
  background-color:transparent;
   border:none; 
  width:80%;
  
  font-family:'Avenir',Arial, Helvetica, sans-serif;
}
.todo-item-edit:focus{
    outline:none;
  }
</style>
