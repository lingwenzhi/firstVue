<template>
  <nav>
    <ul class="pagination">
      <li :class="{'disabled': current == 1}"><a href="javascript:;" @click="setCurrent(current - 1)"> « </a></li>
      <li :class="{'disabled': current == 1}"><a href="javascript:;" @click="setCurrent(1)"> 首页 </a></li>
      <li v-for="p in grouplist" :class="{'active': current == p.val}"><a href="javascript:;"
                                                                          @click="setCurrent(p.val)"> {{ p.text }} </a>
      </li>
      <li :class="{'disabled': current == page}"><a href="javascript:;" @click="setCurrent(page)"> 尾页 </a></li>
      <li :class="{'disabled': current == page}"><a href="javascript:;" @click="setCurrent(current + 1)"> »</a></li>
    </ul>
  </nav>
</template>

<script type="es6">
  export default{
    data(){
      return {
        current: this.currentPage
      }
    },
    props: {
      total: {// 数据总条数
        type: Number,
        default: 0
      },
      display: {// 每页显示条数
        type: Number,
        default: 2
      },
      currentPage: {// 当前页码
        type: Number,
        default: 1
      }
    },
    computed: {
      page: function () { // 总页数
        return Math.ceil(this.total / this.display);
      },
      grouplist: function () { // 获取分页页码
        var len = this.page, temp = [];
          while (len--) {
            temp.push({text: this.page - len, val: this.page - len});
          }
          return temp;
    	}
		},
    methods: {
      setCurrent: function (idx) {
        if (this.current != idx && idx > 0 && idx < this.page + 1) {
          this.current = idx;
          this.$emit('pagechange', this.current);
        }
      }
    }
  }
</script>

<style scoped>
  .pagination {
    overflow: hidden;
    display: table;
    margin: 0 auto;
    /*width: 100%;*/
    height: 50px;
  }
  li {
    list-style-type:none;
    float: left;
    height: 30px;
    border-radius: 5px;
    margin: 3px;
    color: #666;
  }
	a {
    display: block;
    width: 30px;
    height: 30px;
    text-align: center;
    line-height: 30px;
    font-size: 14px;
    border-radius: 5px;
    text-decoration: none;
  }
	.active>a{
		color:blue;
	}
	a{
		color:cadetblue;
	}
	.disabled>a{
		color: #666;
		cursor: not-allowed;
	}
</style>