<!--
We can render content conditionally or in a loop with the v-if and v-for directives.
-->


<!-- <template>
    <button @click="show = !show">Toggle List</button>
  <button @click="list.push(list.length + 1)">Push Number</button>
  <button @click="list.pop()">Pop Number</button>
  <button @click="list.reverse()">Reverse List</button>

  <ul v-if="show && list.length">
    <li v-for="item of list" v-bind:key="item">{{ item }}</li>
  </ul>
  <p v-else-if="list.length">List is not empty, but hidden.</p>
  <p v-else>List is empty.</p>
</template>

    <script>
    export default {
      data() {
        return {
          show: true,
          list: [1, 2, 3]
        }
      }
    }
    </script> -->
    <!--
A simple markdown editor.
-->

<!-- <script>
import { marked } from 'marked'
import { debounce } from 'lodash-es'

export default {
  data: () => ({
    input: '# hello'
  }),
  computed: {
    output() {
      return marked(this.input)
    }
  },
  methods: {
    update: debounce(function (e) {
      this.input = e.target.value
    }, 100)
  }
}
</script>

<template>
  <div class="editor">
    <textarea class="input" :value="input" @input="update"></textarea>
    <div class="output" v-html="output"></div>
  </div>
</template>

<style>
body {
  margin: 0;
}

.editor {
  height: 100vh;
  display: flex;
}

.input,
.output {
  overflow: auto;
  width: 50%;
  height: 100%;
  box-sizing: border-box;
  padding: 0 20px;
}

.input {
  border: none;
  border-right: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
  padding: 20px;
}

code {
  color: #f66;
}
</style> -->


<template>
    <div>
        <div>
            <h1>1</h1>
                <h2>Welcome to my page</h2>
                <p>Here is some content.</p>
        </div>
        <div>
            <h1>2</h1>       
            <div id="selectBox">
                <div> 좋아하는 언어를 선택해보자 </div>
                    <input type="checkbox" value="java" v-model="lang">자바
                    <input type="checkbox" value="C" v-model="lang">C
                    <input type="checkbox" value="C#" v-model="lang">C#
            </div> 
            <div id="selectedLang">선택한 언어 :: <span v-html="lang"></span>
            </div>
        </div>
        <div>
            <h1>3</h1>
                {{ message }}
        </div>
        <div>
            <h1>4</h1>
                <div id="account">숫자 입력
                    <input type="text" v-model="amount">
                        <h2 v-if="amount<0" > 마이너스</h2>
                        <h2 v-else-if="amount>0" > 플러스</h2>
                        <h2 v-else >문자 혹은0</h2> 
                </div>
        </div>
        <div>
            <h1>5</h1>
                <div id="app">
                    {{name}} <br>
                    <button @click="changeName()">change</button>
                </div>
        </div>
        <div>
            <h1>6</h1>
                {{name1}} <br>
                <compo></compo>
        </div>
        <div>
            <h1>7</h1>
                <div id="list">
                    <ul v-for="item in items" v-bind:key="item">
                        <li>{{item.no}}</li>
                        <li>{{item.nm}}</li>
                    </ul>
                </div>
        </div>
        <div>
            <h1>8</h1>
                <button @click="show = !show">Toggle List</button>
                <button @click="list.push(list.length + 1)">Push Number</button>
                <button @click="list.pop()">Pop Number</button>
                <button @click="list.reverse()">Reverse List</button>

                <ul v-if="show && list.length">
                    <li v-for="item of list" v-bind:key="item">{{ item }}</li>
                </ul>
                <p v-else-if="list.length">List is not empty, but hidden.</p>
                <p v-else>List is empty.</p>
        </div>
        <div>
            <h1>9</h1>
            <input type="number" :value="c" @change="setC"> Celsius =
            <input type="number" :value="f" @change="setF"> Fahrenheit
        </div>
        <div>
            <h1>10</h1>
                <div id="app">
                    <span>메시지: {{ msg }}</span>
                </div>
        </div>
        <div>
            <h1>11</h1>
            <div id="app">
                <a v-bind:href="url"> 페이지 이동 </a>
                <br>
                <a v-on:click="doSomething"> url 정보 daum으로 변경  </a>
            </div>
        </div>
    </div>
</template>

<script>
export default({    
    data() {
        return {
            message : "Hello Vue.js~"  ,
            lang : []  ,
           // el : '#selectBox'  ,
            name: 'charlie',
            amount : 0,
            name1 : "charlie_Combo",
            "items" : [
                    { "no" : 1 , "nm" : "아이템1"},
                    {"no" : 2 , "nm" : "아이템2"},
                    {"no" : 3 , "nm" : "아이템3"}
                ],
            show: true,
            list: [1, 2, 3],
            c: 0,
            f: 32,
            msg : '테스트 중',
            url : 'https://m.naver.com/'
                }
            },
    methods: {
        changeName() {
            this.name = this.name + ' changed';
            this.name1 = this.name1 + " changed";
                    },
                    setC(e, c = +e.target.value) {
              this.c = c
              this.f = c * (9 / 5) + 32
            },
            setF(e, f = +e.target.value) {
              this.f = f
              this.c = (f - 32) * (5 / 9)
            },
            doSomething(){
      this.url = 'https://m.daum.net/';
    }
            },
            
                })
                
</script>



