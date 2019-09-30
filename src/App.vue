<template >
<div class="container">
 <div class="row d-flex justify-content-center">
   <div class="col-7 rounded" id="maindiv">
    
  <div class="row backColor">
    <div class="col-12">
      
    <div class="todo-header">
      <app-header    
       
         v-bind:nextId="nextId"
         v-on:clear:list="clearList"
        v-bind:displayBtn="displayBtn"
        ></app-header>
    
    </div>
    </div>  
  </div>
  <div class="row" style="padding:20px;">
    <div class="col-12">
      <todo-input v-on:todo:add="addTodo"></todo-input>
    </div>  
  </div>
      
  <div class="row backColor"> 
    <div class="col-12">   
      <todo-item
        v-for="(todo, index) in todos"
        v-bind:todo="todo"
        v-bind:index="index"
        v-on:todo:remove="removeTodo"
         v-on:edit:done="doneEdit"
        v-on:todo:edit="editTodo"
        v-bind:compare-time="compareTime"
        v-on:change:status="changeStatus(index)"
        :key="todo.id"
      ></todo-item>
      </div>
  </div>
   </div></div></div>

  
</template>
<script>
import AppHeader from "./components/AppHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoItem from "./components/TodoItem.vue";

var moment = require("moment");
moment().format();
export default {
  name: "app",

  components: {
    AppHeader,
    TodoInput,
    TodoItem,
  
  },
  data() {
    return {
      sortedArray:[],
      todos: [
        {
          id: 0,
          text: "database project",
          status: "complete",
          editing:false,
          time: moment("2010-10-20 4:30", "YYYY-MM-DD h:i:s"),
          duedate: moment("2019-11-21 4:30", "YYYY-MM-DD h:i:s")
        },
        {
          id: 1,
          text: "website project",
          status: "uncomplete",
          editing:false,
          time: moment("2010-12-20 4:30", "YYYY-MM-DD h:i:s"),
          duedate: moment("2011-10-2 4:30", "YYYY-MM-DD h:i:s")
        },
        {
          id: 2,
          text: "game project",
          status: "complete",
           editing:false,
          time: moment("2010-11-20 4:30", "YYYY-MM-DD h:i:s"),
          duedate: moment("2019-12-20 4:30", "YYYY-MM-DD h:i:s")
        }
      ],
      status: "",
      nextId: 3,
      beforeEditCache:"",
      displayBtn:true
    };
  },
  mounted: function () {
    this.sortArray();
    },
  
  methods: {
    addTodo(text,duedate) {
    
      this.todos.push({
        id: this.nextId,
        text: text,
        duedate: (duedate != "" ? moment(duedate) : null),
        status: "uncomplete",
        time: moment(),

        editing:false,
      

      });
        

      this.nextId++;
      this.displayBtn=true;
      this.sortArray();
       
  
    },
    removeTodo(index){
      this.todos.splice(index,1);
      
    },
     sortArray()
     { this.sortedArray  = this.todos.sort(function(a,b)
        {
          if(a.duedate < moment()) {
            return 1;
          } else if(a.duedate ===null || b.duedate === null || a.duedate > moment()){
            return -1;
          } else{
            return 0;
          }
        });
        this.todos=this.sortedArray;
      },
    editTodo(todo)
    { this.beforeEditCache=todo.text;
      todo.editing=true;
    },
    doneEdit(todo)
    {
      if(todo.text.trim()==="")
      {
       todo.text=this.beforeEditCache;
      }
       todo.editing=false;
    },
    cancelEdit(todo)
    {
      todo.text=this.beforeEditCache;
     todo.editing=false; 
    },
    clearList()
    {
    
        this.todos=[];
  
        this.nextId=0;
         this.displayBtn=false;
     
    },
    compareTime(index)
    { var currentTime=moment();
       
      var endTime=this.todos[index].duedate;

      if(endTime.isBefore(currentTime))
      {
          if(this.todos[index].status === "uncomplete")
          {
            return true
          }
          else
          {
            return false
          }
      }
      else{
        return false
      }


    },
    changeStatus(index) {
      if (this.todos[index].status === "uncomplete") {
        this.todos[index].status = "complete";
      } else {
        this.todos[index].status = "uncomplete";
      }
    }
  }
};
</script>

<style type="scss">
@import "./App.sass";

</style>