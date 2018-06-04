<template>
  <div class="app-container">
    <el-form class="search-container" :model="filters" :inline="true">
      <span>按内容查询</span>
       <el-input placeholder="请输入内容" v-model="filters.search_input" onkeydown='if(event.keyCode == 13) return false' style="width:200px"></el-input>
       <el-button type="primary" @click="doFilter">搜索</el-button><el-button type="primary" @click="doReset">重置</el-button>
    </el-form>
    <br>
    <el-table :data="copylist" v-loading.body="listLoading" element-loading-text="拼命加载中" border fit max-height="600" id="Detail-table" >
      <el-table-column v-for="(item,key) in Keydata" :label="item.label" :key="key" align="center" :prop="item.value">
      </el-table-column>
    </el-table>  

    <br>
    <div class="block">
      <el-pagination  @current-change="CurrentpageChange" :current-page="currentPage" @size-change="handleSizeChange"
        :page-sizes="[10, 20, 50, 100]" :page-size="pagesize" layout="sizes, prev, pager, next, jumper" :total="len">
      </el-pagination>
    </div>
    <br>
    <el-form :inline="true" class="demo-form-inline">
      <el-radio-group v-model="radio2" @change="choseTime">
        <el-radio :label="-1">全部</el-radio>
        <el-radio :label="1">今天</el-radio>
        <el-radio :label="7">近一周</el-radio>
        <el-radio :label="30">近一个月</el-radio>
        <el-radio :label="0">自定义日期查询</el-radio>
      </el-radio-group>
      <el-form-item label="">
        <el-date-picker v-model="filters.column.create_start_date"  type="date" :picker-options="pickerBeginDateBefore" format="yyyy-MM-dd" placeholder="" :disabled="isfree" value-format="yyyy-MM-dd">
        </el-date-picker>
      </el-form-item>
      <el-form-item label="至" label-width="25px">
        <el-date-picker v-model="filters.column.create_end_date" type="date" :picker-options="pickerBeginDateAfter" placeholder="" :disabled="isfree" @change="timefree" value-format="yyyy-MM-dd">
        </el-date-picker>
      </el-form-item>
      <el-button-group>
        <el-button  @click="changtype('type1')">type1</el-button>
        <el-button  @click="changtype('type2')">type2</el-button>
        <el-button  @click="changtype('type3')">type3</el-button>
        <el-button  @click="changtype('type4')">type4</el-button>
      </el-button-group>
    </el-form>
  </div>
</template>

<script>
//import tabledata from './data'
export default {
  name: 'vue-table-filter',
  data () {
    return {
      currentPage:1,//当前页  
      pagesize:10,//每页显示的条数
      list: null,
      copylist:null,//list的副本
      filterTableDataBefore:[],
      filterTableDataEnd:[],
      datalist:null,
      listLoading: true,
      type:[],//类型数组
      radio2: -1,
      len:0,
      create_time:[],
      searchId:[],
      money:0,
      actualmoney:0,
      fee:0,
      isfree:true,
      filters: {
          search_input:'',
          column: {
              create_start_date: '',
              create_end_date: ''
          },
      },
      pickerBeginDateBefore:{
          disabledDate: (time) => {
              let beginDateVal = this.filters.column.create_end_date;
              if (beginDateVal) {
                  return time.getTime() > beginDateVal;
              }
          }
      },
      pickerBeginDateAfter:{
          disabledDate: (time) => {
              let beginDateVal = this.filters.column.create_start_date;
              if (beginDateVal) {
                  return time.getTime() < beginDateVal;
              }
          }
      },
      result:this.tablevalue,
      Keydata:this.Keyvalue
    }
  },
  props:['tablevalue','Keyvalue'],
  created() {
    this.fetchData()
  },
  methods: {
    fetchData() {
      this.list=this.result
      this.listLoading = false
      this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize)
      this.len=this.list.length 
      this.ss()
    },
    //初始化数据后统计
    ss(){
      this.create_time=[]
      this.searchId=[]
      for(var i=0;i<this.len;i++){
          this.create_time.push(this.list[i].createdAt.slice(0,10))
          this.searchId.push(this.list[i].voucherId)
          this.type.push(this.list[i].voucherType)
      }
    },
    //类型的切换
    changtype(value){
      if(value=="type1"){
        this.typeShow(value)
      }
      else if(value=="type2"){
        this.typeShow(value)
      }
      else if(value=="type3"){
        this.typeShow(value)
      }
      else{
        this.typeShow(value)
      }
    },
    typeShow(value){
      if(this.filterTableDataEnd!=""){//筛选过
        this.filterTableDataBefore=this.filterTableDataEnd
        this.list=[]
        var ll=this.filterTableDataBefore.length
        for(var i=0;i<ll;i++){         
          if(this.type[i]==value){
            this.list.push(this.filterTableDataBefore[i])//重新推入搜索结果
          }
        }
        this.len=this.list.length
        this.ss()//重置数据统计
        this.filterTableDataEnd=this.filterTableDataBefore
      }
      else{//没有筛选过
        this.filterTableDataBefore=this.list
        this.list=[]//清空视图数据
        var ll=this.filterTableDataBefore.length
        for(var i=0;i<ll;i++){         
          if(this.type[i]==value){
            this.list.push(this.filterTableDataBefore[i])//重新推入搜索结果
          }
        }
        this.len=this.list.length
        this.ss()//重置数据统计
        this.filterTableDataEnd=this.filterTableDataBefore
      }
      this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize) 
    },
    //根据页码显示数据
    CurrentpageChange(val){//val是当前页
      this.currentPage = val;
      this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize)
    },
    handleSizeChange(val) {//val是每页的条数
      this.pagesize=val 
      this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize) 
    },
    //日期选择
    timefree(value){
      var start=this.filters.column.create_start_date;
      var end=this.filters.column.create_end_date;
      if(start!=""&&end!=""){
        this.compareTime(start,end)
      }
    },
    choseTime(value){
      var start,end;   
      if(value=="-1"){
        this.isfree=true
        end = new Date()
        start = "Thu Jun 01 1970 00:00:00 GMT+0800 (中国标准时间)"
        this.compareTime(start,end)
        this.filters.column.create_end_date=""
      }
      else if(value=="0"){
        this.isfree=false
      }
      else{
        this.isfree=true
        end = new Date()
        start = new Date()
        start.setTime(start.getTime() - 3600 * 1000 * 24 * value)
        this.compareTime(start,end)
      }
    },
    compareTime(start,end){
      //搜索结果
      if(this.filterTableDataEnd!=""){
        this.filterTableDataBefore=this.filterTableDataEnd
        var ll=this.filterTableDataBefore.length//当前长度
        this.list=[]      
        for(var i=0; i<ll;i++) {
          var ss = new Date(Date.parse(start)),ee = new Date(Date.parse(end));  
          var current=new Date(Date.parse(this.create_time[i]))         
          if(current>=ss && current<=ee){
            this.list.push(this.filterTableDataBefore[i])   
          }
        }
        this.len=this.list.length 
        this.filterTableDataBefore=this.list 
      } 
      else{//没有进行筛选
        this.filterTableDataBefore=this.list
        this.list=[] 
        var ll=this.filterTableDataBefore.length//当前长度
        for(var i=0; i<ll;i++) {  
          var ss = new Date(Date.parse(start)),ee = new Date(Date.parse(end));
          var current=new Date(Date.parse(this.create_time[i]))
          if(current>=ss && current<=ee){
            this.list.push(this.filterTableDataBefore[i])   
          }
        }
        this.len=this.list.length 
        this.filterTableDataEnd=this.filterTableDataBefore   
      } 
      this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize)
    },
    //搜索
    doFilter(){
      if (this.filters.search_input == "") {
        this.$message.warning("查询条件不能为空！");
      return;
      }
      else{
        this.filterTableDataEnd=this.filterTableDataBefore
        this.filterTableDataBefore=this.list
        this.list=[]//清空视图数据  
        for(var i=0;i<this.len;i++){
          var str=JSON.stringify(this.filterTableDataBefore[i]).split(",").join("|").replace(/:/g,"|")
          var arr=str.split("|")
          for(var index=0;index<arr.length;index++){
            if(index%2==0){
              delete arr[index];
            }
          }
          var arr1=arr.join("")
          if(arr1.indexOf(this.filters.search_input)!="-1"){
            this.list.push(this.filterTableDataBefore[i])//重新推入搜索结果
          }
        }
        this.len=this.list.length
        this.ss()//重置数据统计
        this.filterTableDataEnd=this.list
        this.copylist=this.list.slice((this.currentPage-1)*this.pagesize,this.currentPage*this.pagesize)
      } 
    },
    //重置数组
    doReset(){
      if (this.filters.search_input != "") { 
        this.filters.search_input=""
        this.filterTableDataBefore=[]
        this.filterTableDataEnd=[]
      }
       this.fetchData()
    }
   
  }
}
</script>

<style lang="scss">

</style>
