<template>
  <div>
    <h1>ToDoリスト<span class="web-dev">(web開発用)</span></h1>

    <div class="container">
      <section class="main-form">
        <div class="radio-form">
          <input type="radio" v-model="picked" id="direction" value="要件定義">
          <label for="direction">要件定義</label>

          <input type="radio" v-model="picked" id="design" value="デザイン">
          <label for="design">デザイン</label>

          <input type="radio" v-model="picked" id="cording" value="コーディング">
          <label for="cording">コーディング</label>
        </div>
   
        <div class="text-form">
            <label for="text">作業内容: </label>
            <input id="text" type="text" v-model="task" class="text" placeholder="(例)ペルソナ設定">
            <button @click="addList" class="add-btn">追加</button>
        </div>
      </section>


      <section>
        <ul class="todo-list" >
          <li v-for="(todo,index) in todos" :key="todo.id" class="todo">
            <span class="todo-picked">{{ todo.picked }}</span>
            <span class="todo-task">{{ todo.task }}</span>
            <button @click="removeList(index)" class="remove-btn">削除</button>
            <hr>
          </li>
        </ul>
      </section>
      
      <p class="length">全{{ todos.length }}件表示中</p>
      <!-- <p :class="colorChange">色変わるらしい</p> -->

    
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos:[],
      task:"",
      picked:"",
    }
  },
  methods: {
    addList() {
      if(this.task!=="" && this.picked!=="") {
        this.todos.push({
          task:this.task,
          picked:this.picked,
        });
        this.task=""
        this.picked=""
      } else {
        alert('文字を入力、もしくはいずれかのセレクトボタンにチェックしてください。')
      }
      },
    removeList(i) {
      this.todos.splice(i,1)
    },
  },
  mounted() {
    this.todos=JSON.parse(localStorage.getItem('todos')) || [];
  },
  watch: {
    todos: {
      handler() {
      localStorage.setItem('todos',JSON.stringify(this.todos));
      },
      deep:true
    }
  },
}
</script>

<style>
h1 {
  text-align: center;
  margin-top: 50px;
}
.web-dev {
  color: brown;
}
 .container {
   width: 800px;
   margin: 0 auto;
 }
 .select {
   width: 100px;
   background-color: yellow;
 }
 .main-form {
   text-align: center;
   margin-bottom: 40px;
 }
 .radio-form {
   margin-bottom: 10px;
 }
 .text {
   width: 400px;
   height: 30px;
   border-radius: 5px;
   border: 1px solid rgba(0, 0, 0, .5);
   margin-right: 10px;
 }
 .add-btn {
   height: 35px;
   width: 60px;
   border-radius: 5px;
   border: 1px solid rgba(0, 0, 0, .5);
   color: rgb(47, 47, 222);
}

.todo-task {
  width: 500px;
}

.todo-picked {
  width: 100px;
}

 .todo-list {
   list-style: none;
 }

 .todo-list span {
   display: inline-block;
   margin-right: 50px;
 }
 .length {
   text-align: right;
 }

 .red {
   color: red;
 }
 .blue {
   color: blue;
 }

</style>
