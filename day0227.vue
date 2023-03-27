<template>
    <div>
        <div>
            <h1>1</h1>
        </div>
        <ag-grid-vue
    style="width: 500px; height: 200px"
    class="ag-theme-alpine"
    :columnDefs="columnDefs"
    :rowData="rowData">
        </ag-grid-vue>
        <div>
            <h1>2</h1>
            <input v-model="Todo" placeholder="입력하세요" @keyup.enter="addTodo">
            <button @click="addTodo">추가</button>
            <ul>
                <li v-for="(Todo, index) in Todos" :key="index" style="list-style: none;">
                {{ Todo }}
                <button @click="deleteTodo()">삭제</button>
                </li>
            </ul>
        </div>
        <div>
            <h1>3</h1>
            <h2>D-day</h2>
            <div>{{ Day }} 일</div>
            <button v-on:click="Minus">-1</button>
            <button v-on:click="Plus">+1</button>
        </div>
        <div>
            <h1>4</h1>
            <h2>'수수' 찾기</h2>
            <div>{{ message }}</div>
            <button @click="reverse">reverse</button>
            <button @click="add">add</button>
        </div>
        <div>
            <h1>5</h1>
            네이버 <a href="https://www.naver.com/" @click.prevent="notify">https://www.naver.com/</a>
        </div>
        <div>
            <h1>6</h1>
            <!-- red는 되는데 다른 색은 안됨 -->
            <p :class="{red: isRed}" @click="toggleRed">
            Rrrrrrrreeeeeedddddd</p>
            <p :style="{color}" @click="toggleColor">
            Toggle Color</p>
            <p :class="{blue: blue}" @click="Blue">
            Toggle Color</p>
        </div>
        <div>
            <h1>7</h1>
            <input type="checkbox" v-model="checked">
            <span>checked:{{ checked }}</span>
            <br>
            체크하세요:
            <input type="checkbox" v-model="check">
            <span>{{ check }}</span>
        </div>
        <div class="checkbox">
            <h1>8</h1>
            <input type="checkbox" id="james" value="James" v-model="checkedNames">
            <label for="james">James</label>
            <input type="checkbox" id="jack" value="Jack" v-model="checkedNames">
            <label for="jack">Jack</label>
            <input type="checkbox" id="john" value="John" v-model="checkedNames">
            <label for="john">John</label>
            <input type="checkbox" id="mike" value="Mike" v-model="checkedNames">
            <label for="mike">Mike</label>
            <div><span v-html="checkedNames"></span></div>
        </div>
        <div>
            <h1>9</h1>
            <button @click="awesome = !awesome">toggle</button>

            <h1 v-if="awesome">Vue is awesome!</h1>
            <h1 v-else>Oh no 😢</h1>
        </div>
        <div>
            <h1>10</h1>
            <input type="radio" id="one" value="One" v-model="picked">
      <label for="one">One</label>
      <br>
      <input type="radio" id="two" value="Two" v-model="picked">
      <label for="two">Two</label>
      <br>
      <span>Picked: {{ picked }}</span>
        </div>
    </div>
</template>

<script>
import "ag-grid-community/styles/ag-grid.css";
import "ag-grid-community/styles/ag-theme-alpine.css";
import { AgGridVue } from "ag-grid-vue3";


export default {
    data() {
        return {
            columnDefs: null,
            rowData: null,
            gridOptions: null,
            ticketData: [],
            // Todo:'',
            Todos:[],
            Day: 0,
            message: '수박',
            isRed: true,
            color: 'skyblue',
            blue: true,
            checked: false,
            check: true,
            checkedNames: [],
            awesome: true,
            picked: 'One'
              }
            },
        components: {
            AgGridVue
        },

        created() {
            this.columnDefs = [
                { field: 'id' },
                { field: 'title' },
                { field: 'userId' },
                { field: 'completed'}
            ];
            this.$axios
       .get('https://jsonplaceholder.typicode.com/todos/1')
       

       .then((res) => {
        this.rowData = [res.data];
    })
},
    methods: {
        addTodo() {
            this.Todos.push(this.Todo);
            this.Todo='';
        },
        deleteTodo(index) {
            this.Todos.splice(index, 1);
          },
        Minus: function() {
            this.Day--;
        },
        Plus: function() {
            this.Day++;
        },
        reverse() {
            this.message = this.message.split('').reverse().join('')
        },
        add() {
            this.message += '수박'
        },
        notify() {
            alert('탐색이 차단되었습니다. ')
        },
        toggleRed() {
            this.isRed =! this.isRed
        },
        toggleColor() {
            this.color = this.color === 'skyblue' ? 'purple' : 'skyblue',
            this.color = this.color === 'purple' ? 'yellow' : 'purple'
        },
        Blue() {
            this.blue =! this.blue
        },
        // Name() {
        //     this.checkbox = this.checkbox.split('').join('')
        // }
        }
    }
    
</script>

<style>
/* h2 {color: maroon;} */
</style>