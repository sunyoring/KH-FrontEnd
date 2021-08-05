<template>
    <div class="container">
        <h2>Todo List</h2>
        <div class="input-group" style="margin-bottom:10px;">
            <input type="text" class="form-control" 
                placeholder="할일을 입력하세요" 
                v-model="name" 
                v-on:keyup.enter="createTodo(name)">
            <span class="input-group-btn">
                <button class="btn btn-default" type="button" 
                @click="createTodo(name)">추가</button>
            </span>
        </div>
        <ul class="list-group">
            <li :key="index" class="list-group-item" v-for="(todo, index) in todos">
             {{todo.name}} 	


            <div class="btn-group pull-right" 
                style="font-size: 12px; line-height: 1;">
              
            
                 
                  <a href="#" @click="deleteTodo(todo,index)">삭제</a>
                <!-- <a href="#" @click="deleteTodo(index)">삭제</a> -->
            </div>
          
            </li>
        </ul>
    </div>
</template>
<script>
export default{
 data() {
     return{
         name:'',
         todos:[
             /*
            {name:'vue 수업'},
            {name:'bootstrap 수업'},
            {name:'servlet 수업'},
            {name:'jsp 수업'}
            */
         ]
     }
 },
 mounted(){ //JSON으로 값 가져올 것.
     this.getTodos();
 },
 methods:{
     /*deleteTodo(i){ //i로받아옴
         this.todos.splice(i,1); //this.todos. 에서 받아서 i부터 1개
     }*/
     deleteTodo(todo, i){
         this.$ax.delete('http://localhost:3000/data:/' + todo.id)
         .then((result)=>{
             this.todos.splice(i,1);
             console.log(result.data)
         })
     }
     ,
     createTodo(name){
        /* if(name != null){
             this.todos.push({name:name});
             this.name = null;
         }
         */

        if(name != null){
            this.$ax.defaults.headers.post['Content-Type'] = 'application/json'; //json으로 가져올때는 명시해줘야함
            this.$ax.post('http://localhost:3000/data:',{
                name:name  //json서버 자체에서 아이디값을 숫자로 해놓으면 기본적으로 1씩 중감시키게 되어있다. //문자열로 하면 알수없는 문자열로 들어가짐.
            }).then((result)=>{
            this.todos.push(result.data)
         })
         this.name = null

        }
     },
     getTodos(){
         this.$ax.get('http://localhost:3000/data:')
         .then((result)=>{
            this.todos = result.data
            console.log(result)
            console.log(result.data)
         })   
     }
 }
}

</script>
