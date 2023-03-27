<template>
    <div>
        <div>
            <h1>1</h1>
            <div id="account">숫자 입력
                    <input type="text" v-model="amount">
                        <h2 v-if="amount<0" > -</h2>
                        <h2 v-else-if="amount>0" > +</h2>
                        <h2 v-else >문자 혹은0</h2> 
            </div>
        </div>
        <div>
            <h1>2</h1>
                <div id="app">
                    <a v-bind:href="url">네이버 </a>
                    <br>
                    <a v-on:click="doSomething"> 모바일로 변경  </a>
                </div>
        </div>
        <div>
            <h1>3</h1>
                <div>짝맞추기
                    <br>
                    
                    <button @click="insert">insert</button>
                    <button @click="shuffle">shuffle</button>
                   <div style="display: inline;">
                        <div v-for="name in names" class="name" :key="name" >{{ name }}
                        <div v-for="item in items" class="item" :key="item">
                            {{ item }}    
                            <!-- <input for="john" v-model="checkedNames"></input> -->
                            <button @click="remove(item)">x</button>
                        </div>               
                        </div>                         
                    </div>
                </div>
        </div>
        <div>
            <h1>4</h1>
            <p :class="{ red: isRed }" @click="getData">
               클릭하세요 {{kkk}} {{ title }}
              </p>
        </div>
        <div>
            <h1>5</h1>
            <br>
            {{ text }}
            <br>
            <input v-model="text"> 
        </div>
    </div>
</template>

<!-- <script src="https://unpkg.com/ag-grid/dist/ag-grid.min.js"></script> -->
<script>
//import { jSXNamespacedName } from '@babel/types'
import { shuffle } from 'lodash-es'
const getInitialItems = () => [1 , 2, 3, 4, 5 ]
let id = getInitialItems().length + 1
const getInitialNames = () => ['james', 'john', 'mack', 'lana', 'jack']

    export default ({
        data() {
            return {        
                amount: 0,
                url : 'https://www.naver.com/',
                items: getInitialItems(),
                names:  getInitialNames(),
                kkk: "",
                title: "",
                text: ""
            }
        },
        methods: {
            doSomething(){
      this.url = 'https://m.naver.com/';
      
    },
    insert() {
      const i = Math.round(Math.random() * this.items.length)
      this.items.splice(i, 0, id++)
    },
    reset() {
      this.items = getInitialItems()
    },
    shuffle() {
      this.items = shuffle(this.items)
    },
    remove(item) {
      const i = this.items.indexOf(item)
      if (i > -1) {
        this.items.splice(i, 1)
      }
    }, 
    getData() {
     
     this.$axios
       .get('https://jsonplaceholder.typicode.com/todos/3')
       .then((res) => {
        // var aaa = JSON.parse(JSON.stringify(res.data))
         this.kkk = res.data["id"];
         this.title = res.data["title"];
         alert("id=>" + res.data["id"] );
         console.log(res.staus);
         console.log(res.data);
       })
       .catch((error) => {
         console.log(error);
       })
       .finally(() => {
         console.log("항상 마지막에 실행");
       });
   },      
}
    })
</script>