<template>
  <div class="first">
    <input type="text" v-model="searchMsg" @keyup="setTotalLength">
   <center>
      <table >
        <tr>
          <td>序号</td>
          <td>姓名</td>
          <td>年龄</td>
        </tr>
        <tr v-for="msg in pageData">
          <td>{{msg.id}}</td>
          <td>{{msg.name}}</td>
          <td>{{msg.age}}</td>
        </tr>
      </table>
   </center>
  <page :total="total" @pagechange="pagechange"></page>
  </div>
</template>

<script>
import Page from './Page'
export default {
  name: 'first',
  data () {
    return {
      tableMessage: [{
        id: 1,
        name: 'peng',
        age: 20
      },
      {
        id: 2,
        name: 'zhang',
        age: 21
      },
      {
        id: 3,
        name: 'wang',
        age: 22
      },
      {
        id: 4,
        name: 'li',
        age: 22
      },
      {
        id: 5,
        name: 'sun',
        age: 20
      },
      {
        id: 6,
        name: 'zhao',
        age: 22
      }],
      searchMsg: '',
      total: 6,
      current: 1,
      display: 2
    }
  },
  computed: {
    namefilter: function (value) {
      var key = this.searchMsg
      var data = this.tableMessage
      return data.filter(function (item) {
        return item.name.indexOf(key) !== -1
      })
    },
    pageData: function () {
      var temp = []
      var index = (this.current - 1) * this.display
      var showData = this.namefilter
      for (var i = 0; i < this.display; i++) {
        if (index + i < this.namefilter.length) temp.push(showData[index + i])
      }
      return temp
    }
  },
  methods: {
    setTotalLength: function () {
      this.total = this.namefilter.length
      this.current = 1
    },
    pagechange: function (currentPage) {
      this.current = currentPage
    }
  },
  components: {
    Page
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table{
  width:400px;
  border:0;
  text-align: center;
}
td{
  width:133px;
}
</style>
