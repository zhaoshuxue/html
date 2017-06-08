
# 表格插件 BootstrapTable

#### 官网地址： [http://bootstrap-table.wenzhixin.net.cn/zh-cn/](http://bootstrap-table.wenzhixin.net.cn/zh-cn/)

#### Github地址： [https://github.com/wenzhixin/bootstrap-table](https://github.com/wenzhixin/bootstrap-table)


> 官网介绍：
> 基于 Bootstrap 的 jQuery 表格插件，通过简单的设置，就可以拥有强大的单选、多选、排序、分页，以及编辑、导出、过滤（扩展）等等的功能。


##### 主要功能

- 支持 Bootstrap 3 和 Bootstrap 2
- 自适应界面
- 固定表头
- 非常丰富的配置参数
- 直接通过标签使用
- 显示/隐藏列
- 显示/隐藏表头
- 通过 AJAX 获取 JSON 格式的数据
- 支持排序
- 格式化表格
- 支持单选或者多选
- 强大的分页功能
- 支持卡片视图
- 支持多语言
- 支持插件

## 优点

- 学习成本较低，配置简单，文档齐全
- 跟Bootstrap无缝衔接，整体风格一致，也便于二次开发
- 开发者活跃，Github定期维护




## 开始使用


- 1、在网页的head标签里插入下面的代码

```
<!-- 引入bootstrap样式 -->
<link href="https://cdn.bootcss.com/bootstrap/3.3.6/css/bootstrap.min.css" rel="stylesheet">
<!-- 引入bootstrap-table样式 -->
<link href="https://cdn.bootcss.com/bootstrap-table/1.11.1/bootstrap-table.min.css" rel="stylesheet">

<!-- jquery -->
<script src="https://cdn.bootcss.com/jquery/2.2.3/jquery.min.js"></script>
<script src="https://cdn.bootcss.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>

<!-- bootstrap-table.min.js -->
<script src="https://cdn.bootcss.com/bootstrap-table/1.11.1/bootstrap-table.min.js"></script>
<!-- 引入中文语言包 -->
<script src="https://cdn.bootcss.com/bootstrap-table/1.11.1/locale/bootstrap-table-zh-CN.min.js"></script>

```

- 2、在页面body代码块里定义表格展示的区域

```
<table id="table"></table>

```

- 3、编写JavaScript代码渲染表格

在网页代码最下面插入js脚本，内容如下：

```

$("#table").bootstrapTable({ // 对应table标签的id
      url: "<%=request.getContextPath()%>/api/getDataList.do", // 获取表格数据的url
      cache: false, // 设置为 false 禁用 AJAX 数据缓存， 默认为true
      striped: true,  //表格显示条纹，默认为false
      pagination: true, // 在表格底部显示分页组件，默认false
      pageList: [10, 20], // 设置页面可以显示的数据条数
      pageSize: 10, // 页面数据条数
      pageNumber: 1, // 首页页码
      sidePagination: 'server', // 设置为服务器端分页
      queryParams: function (params) { // 请求服务器数据时发送的参数，可以在这里添加额外的查询参数，返回false则终止请求

          return {
              pageSize: params.limit, // 每页要显示的数据条数
              offset: params.offset, // 每页显示数据的开始行号
              sort: params.sort, // 要排序的字段
              sortOrder: params.order, // 排序规则
              dataId: $("#dataId").val() // 额外添加的参数
          }
      },
      sortName: 'id', // 要排序的字段
      sortOrder: 'desc', // 排序规则
      columns: [
          {
              checkbox: true, // 显示一个勾选框
              align: 'center' // 居中显示
          }, {
              field: 'stdCode', // 返回json数据中的name
              title: '标准编号', // 表格表头显示文字
              align: 'center', // 左右居中
              valign: 'middle' // 上下居中
          }, {
              field: 'stdName',
              title: '标准名称',
              align: 'center',
              valign: 'middle'
          }, {
              field: 'calcMode',
              title: '计算方式',
              align: 'center',
              valign: 'middle',
              formatter: function (value, row, index){ // 单元格格式化函数
                  var text = '-';
                  if (value == 1) {
                      text = "固定";
                  } else if (value == 2) {
                      text = "阶梯";
                  } else if (value == 3) {
                      text = "区间";
                  } else if (value == 4) {
                      text = "金额";
                  }
                  return text;
              }
          }, {
              title: "操作",
              align: 'center',
              valign: 'middle',
              width: 160, // 定义列的宽度，单位为像素px
              formatter: function (value, row, index) {
                  return '<button class="btn btn-primary btn-sm" onclick="del(\'' + row.stdId + '\')">删除</button>';
              }
          }
      ],
      onLoadSuccess: function(){  //加载成功时执行
            console.info("加载成功");
      },
      onLoadError: function(){  //加载失败时执行
            console.info("加载数据失败");
      }

})


```










----------------------