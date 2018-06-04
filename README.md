# vue-tablefilter
===
### filter tables based on conditions（根据条件筛选表格）
##### 主要思路：根据选定的条件对表格中已有的数据进行过滤，符合条件的推入新的数组，这种适合数据量不大，或者筛选的字段较为简单，如果数据量太大，或者字段需多次处理才有结果的会严重拖慢筛选过程。  
##### 功能描述：搜索表格内容、根据时间段或者自定义时间筛选、类型筛选

download直接下载查看  
>`npm install`  
>`npm run dev`

使用npm install，在main.js或者其他组件里面  
>`npm install vue-table-filter`   
>`import from "vue-table-filter"`  

里面的主要传值是tablevalue保存表格字段的内容,Keyvalue保存表格的label值和对应显示的字段值
