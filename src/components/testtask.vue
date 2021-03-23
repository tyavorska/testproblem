<template>
  <div class="hello">
    <div class="inputs">
      <input v-model="inpDate" type="date">
      <input v-model="inpCost" type="text">
      <input v-model="inpCurrency" type="text">
      <input v-model="inpName" type="text">
      <button @click="addMethod()">{{add}}</button>
    </div>

    <div class="list">
      <ul class="addlist" >
        <li v-for="(item, index) in uniqueKeys" :key="item">
          <p class="bold">{{item}}</p>
          <p v-for="product in items[index][item]" :key="product.id">
            {{product.cost}} {{product.currency}} {{product.name}}
          </p>
          <button v-on:click="uniqueKeys.splice(index, 1)">{{clear}}</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Testtask',
  props: {
    msg: String
  },
  data() {
    return {
      keyArr: [],
      add: 'add',
      clear: 'clear',
      inpDate: null,
      inpCost: null,
      inpCurrency: null,
      inpName: null,
      items: [],
      obj: {},
      uniqueKeys: [],
      ids: [],
    }
  },
  methods: {
    addMethod() {
      let myDate = this.inpDate
      if(!this.uniqueKeys.includes(myDate)) {
        this.uniqueKeys.push(myDate)
      }

      for (let i = 0; i < this.items.length; i++) {
        let keys = Object.keys(this.items[i])
        this.keyArr.push(keys[0])
      }

      if (this.keyArr.includes(this.inpDate)) {
        for (let i = 0; i < this.items.length; i++) {
          if (Object.keys(this.items[i])[0] == this.inpDate) {

            let innerObj = {}
            innerObj["cost"] = this.inpCost
            innerObj["currency"] = this.inpCurrency
            innerObj["name"] = this.inpName
            innerObj["id"] = this.ids.length + 1
            this.ids.push(innerObj["id"])
            this.items[i][myDate].push(innerObj)

          }
        }
      } else {
        let obj = {}
        obj[myDate] = []
        let innerObj = {}
        innerObj["cost"] = this.inpCost
        innerObj["currency"] = this.inpCurrency
        innerObj["name"] = this.inpName
        innerObj["id"] = this.ids.length + 1
        this.ids.push(innerObj["id"])
        obj[myDate].push(innerObj)
        this.items.push(obj)
      }
    }
  }
}
</script>

<style>
body {
  background: #dadada;
}

h3 {
  margin: 40px 0 0;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.bold{
  font-weight: bold;
}
.flex{
  display: flex;
}
input {
  border: navajowhite;
  border-radius: 5px;
  margin-right: 20px;
  padding: 10px;
  width: 200px;
}
button {
  color: #26ABA2;
  font-size: 16px;
  border: 1px solid #26ABA2;
  border-radius: 5px;
  cursor: pointer;
  width: 212px;
  padding: 6px;
}
button:hover {
  background-color: #26ABA2;
  color: #fff;
}
</style>