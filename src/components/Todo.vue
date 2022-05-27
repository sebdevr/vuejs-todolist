<template>
  <div class="container">
    <h1>Vue To-do list</h1>
        <b-list-group class="listGroup">
      <b-list-group-item
        class="listGroupItem"
        v-for="(item, index) in filteredArray"
        v-bind:key="index"
        :class="{ active: item.done === true }" >
        <span>{{ index + 1 }} -</span>
        {{ item.text }}
        <button class="removeButton" @click="removeItem(index);">X</button>
        <button class="checkButton" @click="changeStatus(item);">Done</button>
      </b-list-group-item>
    </b-list-group>
    <input type="text" placeholder="Add a task..." v-model="word" @keyup.enter="addWord">
  </div>
</template>

<script>
export default {
  name: "Todo",
  created: function(){
      this.filteredArray = [...this.todoArray];
  },
  data() {
    return {
      count: 0,
      word: "",
      todoArray: [
      ],
      filteredArray: []
    };
  },
  methods: {
    addWord: function() {
      if (this.word !== "") {
        this.todoArray.push({ text: this.word, done: false });
        this.word = "";
        this.filterArray();
      }
    },
    removeItem: function(idx) {
      let prevWordArray = [...this.todoArray];
      prevWordArray.splice(idx, 1);
      this.todoArray = prevWordArray;
      this.filterArray();
    },
    changeStatus: function(itm) {
      let clickedElem = this.todoArray.find(item => {
        return item.text === itm.text;
      });
      clickedElem.done = clickedElem.done === false;
      this.filterArray();
    },
    filterArray: function(type) {
        if (type === "active") {
            this.filteredArray = this.todoArray.filter(item => {
                return item.done === false;
            })
        } else if (type === 'complete'){
            this.filteredArray = this.todoArray.filter(item => {
                return item.done === true;
            })
        } else {
            this.filteredArray = this.todoArray;
        }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.listGroup {
  width: 80%;
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
}
.container {
margin-top: 8em;
border: solid 1px;
background: white;
border-radius: 20px;
width: 70%;
padding: 0.5em;
}

span {
  color: purple;
  font-weight: bold;
}

input[type="text"] {
  margin-top: 20px;
  padding: 8px 8px 8px 50px;
  border-radius: 5px;
  border: 1px solid black;
  
}

.listGroupItem {
  text-align: left;
  margin: 10px 0px;
}

.addButton {
  margin-left: 10px;
  padding: 5px 10px;
  background-color: white;
  border: 1px solid black;
  color: black;
  border-radius: 3px;
}

.removeButton {
  color: white;
  font-weight: bold;
  background-color: red;
  border: 1px solid red;
  font-size: 14px;
  height: 30px;
  width: 30px;
  border-radius: 6px;
  border: 1px solid black;
  float: right;
  transition: background-color 0.5s, color 0.5s;
}

.checkButton {
  float: right;
  font-size: 14px;
  margin-right: 10px;
  background: white;
  height: 30px;
  width: 50px;
 border: 1px solid black;
 border-radius: 6px;
 border: 1px solid black;
  
}

.checkIcon:hover {
  cursor: pointer;
}

.removeButton:hover {
  cursor: pointer;
  background-color: white;
  color: red;
}

.active {
  text-decoration-line: line-through;
  background-color: white;
  border-color: black;
  color: green;
}

.pointy {
  cursor: pointer;
}
</style>
