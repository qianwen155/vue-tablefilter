<template>
  <div id="app">
    <h1>{{ msg }}</h1>
    <h2>Essential Links</h2>
    <tableFilter :tablevalue="result" :Keyvalue="Keydata"></tableFilter>
  </div>
</template>

<script>
import tableFilter from './lib/vue-table-filter'
export default {
  name: 'app',
  components:{tableFilter},
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      result:[
        {
          id:'123',
          name:'小一',
          phone:'1234579456',
          createdAt:'2018-04-12 04:47:40',
          voucherId:'6541785132465',
          voucherType:'type1'
        },
        {
          id:'124',
          name:'禅城',
          phone:'1234579456',
          createdAt:'2018-04-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type1'
        },
        {
          id:'125',
          name:'小而',
          phone:'1218579456',
          createdAt:'2018-05-22 04:47:40',
          voucherId:'6799445424545',
          voucherType:'type1'
        },
        {
          id:'126',
          name:'小手动',
          phone:'1234579456',
          createdAt:'2018-04-22 09:47:40',
          voucherId:'6787123454545',
          voucherType:'type2'
        },
        {
          id:'127',
          name:'小asd',
          phone:'1234579456',
          createdAt:'2018-09-22 04:47:40',
          voucherId:'6777441234545',
          voucherType:'type3'
        },
        {
          id:'128',
          name:'小ef',
          phone:'1234579456',
          createdAt:'2018-10-22 04:47:40',
          voucherId:'6787123424545',
          voucherType:'type2'
        },
        {
          id:'129',
          name:'小一',
          phone:'1234579456',
          createdAt:'2018-04-22 04:03:40',
          voucherId:'6787445334545',
          voucherType:'type4'
        },
        {
          id:'130',
          name:'小efe',
          phone:'1234777456',
          createdAt:'2018-04-22 17:47:40',
          voucherId:'6783345424545',
          voucherType:'type1'
        },
        {
          id:'131',
          name:'小qasa',
          phone:'1233339456',
          createdAt:'2018-04-22 04:07:50',
          voucherId:'6787445424335',
          voucherType:'type3'
        },
        {
          id:'132',
          name:'小qew',
          phone:'1234333456',
          createdAt:'2018-04-01 21:47:40',
          voucherId:'6787445424000',
          voucherType:'type1'
        },
        {
          id:'133',
          name:'小sfaf',
          phone:'1234579456',
          createdAt:'2018-04-18 14:37:40',
          voucherId:'6700000424545',
          voucherType:'type4'
        },
        {
          id:'134',
          name:'小cvb',
          phone:'1234579456',
          createdAt:'2018-06-22 04:01:00',
          voucherId:'6787445424005',
          voucherType:'type2'
        },
        {
          id:'135',
          name:'小efaaa',
          phone:'1234579456',
          createdAt:'2018-02-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type2'
        },
        {
          id:'136',
          name:'小edc',
          phone:'1234579456',
          createdAt:'2018-04-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type1'
        },
        {
          id:'136',
          name:'小edc',
          phone:'1234579456',
          createdAt:'2018-04-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type1'
        },
        {
          id:'136',
          name:'小edc',
          phone:'1234579456',
          createdAt:'2018-04-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type3'
        },
        {
          id:'136',
          name:'小edc',
          phone:'1234579456',
          createdAt:'2018-04-22 04:47:40',
          voucherId:'6787445424545',
          voucherType:'type4'
        }
      ],
      Keydata:[
        {label:'内部账户',value:'id'},
        {label:'名称',value:'name'},
        {label:'手机号',value:'phone'},
        {label:'创建时间',value:'createdAt'},
        {label:'编号',value:'voucherId'},
        {label:'类型',value:'voucherType'}
      ]
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
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
</style>
