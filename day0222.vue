<template>
    <div>
        <div>
        <h1>1</h1>
            <button @click="insert">insert at random index</button>
            <button @click="reset">reset</button>
            <button @click="shuffle">shuffle</button>

            <TransitionGroup tag="ul" name="fade" class="container">
                <div v-for="item in items" class="item" :key="item">
                    {{ item }}
                    <button @click="remove(item)">x</button>
                </div>
            </TransitionGroup>
            </div>
            <div>
                <h1>2</h1>

                  <button @click="toggleShow">
                  <span v-if="isShowing">Hide child</span>
                  <span v-else>Show child</span>
                  </button>
            </div>
            <div>
              <h1>3</h1>
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
              <h1>4</h1>
                <p>{{ count }}번</p>
                <button v-on:click="countUp">+</button>
                <button v-on:click="countDown">-</button>
            </div>
            <div>
              <h1>5</h1>
              <h2>{{message}}</h2>
              <button @click="reverseMessage">Reverse</button>
              <button @click="message += '~!'">Append "~!"</button>
            </div>
            <div>
              <h1>6</h1>
              <p :class="{ red: isRed }" @click="toggleRed">
                This should be red... but click me to toggle it.
              </p>
            
              <!-- style bindings also support object and arrays -->
              <p :style="{ color }" @click="toggleColor">
                This should be green, and should toggle between green and blue on click.
              </p>
            </div>
            <div>
              <h1>7</h1>
                <input v-model="text"> {{ text }}
            </div>

            <p :class="{ red: isRed }" @click="getData">
               222222222222 {{kkk}} {{ title }}
              </p>
    </div>
</template>

<script>
import { shuffle } from 'lodash-es'

const getInitialItems = () => [1, 2, 3, 4, 5]
let id = getInitialItems().length + 1
// const Child = {
//  template: '#childarea',
//  beforeCreate() {
// console.log("beforeCreate!");
//  }, 
//  created() {
// console.log("created!");
//  }, 
//  beforeMount() {
// console.log("beforeMount!");
//  }, 
//  mounted() {
// console.log("mounted!");
//  }, 
//  beforeDestroy() {
// console.log("beforeDestroy!");
//  }, 
//  destroyed() {
// console.log("destroyed!");
//  }
// 		};

export default {
  
  data() {
    return {
      items: getInitialItems(),
      isShowing: false ,
      newTodo: '',
          todos: [],
          count:0,
          message: 'Hello World!',
          isRed: true,
          color: 'blue',
          text: 'Edit me',
          kkk: "",
          title: ""
    }
  },
  methods: {
    getData() {
     
      this.$axios
        .get('https://jsonplaceholder.typicode.com/todos/3')
        .then((res) => {
         // var aaa = JSON.parse(JSON.stringify(res.data))
          this.kkk = res.data["id"];
          this.title = res.data["title"];
          alert("id=====>" + res.data["id"] );
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
    toggleShow() {
  this.isShowing = !this.isShowing;
			},
      addTodo() {
            this.todos.push(this.newTodo);
            this.newTodo = '';
          },
          deleteTodo(index) {
            this.todos.splice(index, 1);
          },
          countUp: function() {
            this.count++;},
            countDown: function() {
              if(this.count>0) {
                this.count--;
              }
          },
          reverseMessage() {
          this.message = this.message.split('').reverse().join('')
        },
        toggleRed() {
          this.isRed = !this.isRed
        },
        toggleColor() {
          this.color = this.color === 'blue' ? 'purple' : 'green',
          this.color = this.color === 'green' ? 'pink' : 'yellow',
          this.color = this.color === 'pink' ? 'brown' : 'yellow'},
          

  }
}
</script>

<style>
.container {
  position: relative;
  padding: 0;
}

.item {
  width: 100%;
  height: 30px;
  background-color: #f3f3f3;
  border: 1px solid #666;
  box-sizing: border-box;
}

/* 1. declare transition */
.fade-move,
.fade-enter-active,
.fade-leave-active {
  transition: all 0.5s cubic-bezier(0.55, 0, 0.1, 1);
}

/* 2. declare enter from and leave to state */
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: scaleY(0.01) translate(30px, 0);
}

/* 3. ensure leaving items are taken out of layout flow so that moving
      animations can be calculated correctly. */
.fade-leave-active {
  position: absolute;
}
body {
	font-family: "Malgun Gothic","맑은 고딕", serif;
	}

	#app {
	text-align: center;
	margin: 60px;
	max-width: 400px;
	margin: 0 auto;
	display: table;
	}

	.num {
	color: #AF007E;
	}

	button {
	font-family: 'Bitter';
	background: #c62735;
	color: white;
	border: 0;
	padding: 5px 15px;
	margin: 0 10px;
	border-radius: 4px;
	outline: 0;
	cursor: pointer;
	}

	h4 {
	margin: 0 0 15px;
	}

	hr {
	border-color: #F2FAFF;
	opacity: 0.5;
	margin: 15px 0;
	}
</style>