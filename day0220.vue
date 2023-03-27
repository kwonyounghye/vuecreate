<template>
    <div>
      <div class="header">
        <h1>1</h1>
      <input v-model="newTodo" placeholder="할 일을 입력하세요" @keyup.enter="addTodo">
      <button @click="addTodo()">추가</button>
      <ul>
        <li v-for="(todo, index) in todos" :key="index" style=" list-style-type: none;">
          {{ todo }}
          <button @click="deleteTodo(index)">삭제</button>
        </li>
      </ul>
    </div>
    <div>
      <h1>2</h1>
      <h2>클릭하면 카운터가 올라갑니다.</h2>
      <p>{{ count }}회</p>
      <button v-on:click="countUp">카운터+</button>
      <button v-on:click="countDown">카운터-</button>
    </div>
    <h1>3</h1>
    <h2>{{ message }}</h2>
     <!--
        Bind to a method/function.
        The @click syntax is short for v-on:click.
      -->
      <h1>4</h1>
      <button @click="reverseMessage">Reverse Message</button>
    
      <!-- Can also be an inline expression statement -->
      <button @click="message += '!'">Append "!"</button>
    
      <!--
        Vue also provides modifiers for common tasks
        such as e.preventDefault() and e.stopPropagation()
      -->
      <a href="https://vuejs.org" @click.prevent="notify">
        A link with e.preventDefault()
      </a>
      <h1>5</h1>
      <p>
        <span :title="message">
          Hover your mouse over me for a few seconds to see my dynamically bound title!
        </span>
      </p>
    
      <!--
      class bindings have special support for objects and arrays
      in addition to plain strings
      -->
      <p :class="{ red: isRed }" @click="toggleRed">
        This should be red... but click me to toggle it.
      </p>
    
      <!-- style bindings also support object and arrays -->
      <p :style="{ color }" @click="toggleColor">
        This should be green, and should toggle between green and blue on click.
      </p>
      <!-- <button @click="show = !show">Toggle List</button>
      <button @click="list.push(list.length + 1)">Push Number</button>
      <button @click="list.pop()">Pop Number</button>
      <button @click="list.reverse()">Reverse List</button>
    
      <ul v-if="show && list.length">    
        <li v-for="item of list">{{ item }}</li>
      </ul>
      <p v-else-if="list.length">List is not empty, but hidden.</p>
      <p v-else>List is empty.</p> -->
      <h1>6</h1>
      <h2>Text Input</h2>
      <input v-model="text"> {{ text }}
      <h1>7</h1>
      <h2>Checkbox</h2>
      <input type="checkbox" id="checkbox" v-model="checked">
      <label for="checkbox">Checked: {{ checked }}</label>
    
      <!--
        multiple checkboxes can bind to the same
        array v-model value
      -->
      <h1>8</h1>
      <h2>Multi Checkbox</h2>
      <input type="checkbox" id="james" value="James" v-model="checkedNames">
      <label for="james">James</label>
      <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
      <label for="jack">Jack</label>
      <input type="checkbox" id="john" value="John" v-model="checkedNames">
      <label for="john">John</label>
      <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
      <label for="mike">Mike</label>
      <p>Checked names: {{ checkedNames }}</p>
      <h1>9</h1>
      <h2>Radio</h2>
      <input type="radio" id="one" value="One" v-model="picked">
      <label for="one">One</label>
      <br>
      <input type="radio" id="two" value="Two" v-model="picked">
      <label for="two">Two</label>
      <br>
      <span>Picked: {{ picked }}</span>
      <h1>10</h1>
      <h2>Select</h2>
      <select v-model="selected">
        <option disabled value="">Please select one</option>
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
      <span>Selected: {{ selected }}</span>
      <h1>11</h1>
      <h2>Multi Select</h2>
      <select v-model="multiSelected" multiple style="width:100px">
        <option>A</option>
        <option>B</option>
        <option>C</option>
      </select>
      <span>Selected: {{ multiSelected }}</span>
    </div>
    </template>
    
    <script>
    
      export default {
      el: "#app",
        data() {
          return {
            text: 'Edit me',
            checked: true,
            checkedNames: ['James'],
            picked: 'One',
            selected: 'A',
            multiSelected: ['A'],
            //   show: true,
            // list: [1, 2, 3],
            message: 'Hello World!',
            isRed: true,
            color: 'green',
            count:0,
            newTodo: '',
            todos: []
        }},
        methods: {
          toggleRed() {
            this.isRed = !this.isRed
        },
          toggleColor() {
            this.color = this.color === 'green' ? 'blue' : 'green'},
          reverseMessage() {
            this.message = this.message.split('').reverse().join('')
        },
          notify() {
            alert('navigation was prevented.')
        },
          countUp: function() {
            this.count++;},
          countDown: function() {
              if(this.count>0) {
                this.count--;
              }
          },
        addTodo() {
            this.todos.push(this.newTodo);
            this.newTodo = '';
          },
        deleteTodo(index) {
            this.todos.splice(index, 1);
          }
         } }
    </script>
    
    <style>
    #app {
      font-family: Avenir, Helvetica, Arial, sans-serif;
      -webkit-font-smoothing: antialiased;
      -moz-osx-font-smoothing: grayscale;
      text-align: center;
      color: #2c3e50;
      margin-top: 60px;
    }
    .red {
      color: red;
    }
    </style>
    