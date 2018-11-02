<template>
  <div class="demo1">
    <div class="header">
      <el-row :gutter="20">
        <el-col :span="4">
          <div class="select-module">
            <div class="title">选择可视化表</div>
            <el-select v-model="value1" placeholder="请选择" style="width: 100%;">
              <el-option
                v-for="item in value1Options"
                :key="item.value"
                :label="item.label"
                :value="item.value">
              </el-option>
            </el-select>
          </div>
        </el-col>
        <el-col :span="20">
          <div class="title">Custom Report</div>
          <div class="dragDrop-module">
            <draggable v-model="newArr" element="div">
              <el-tag
              v-for="tag in newArr"
              :key="tag.label"
              :closable="true"
              @close="delTag(tag)"
              :type="tag.type">
              {{tag.label}}
              </el-tag>
            </draggable>
          </div>
        </el-col>
      </el-row>
    </div>
    <div class="main">
      <el-row :gutter="20">
        <el-col :span="4">
          <div class="title">维度</div>
          <div class="scroll-box">
            <el-scrollbar style="height: 100%">
              <ul class="dimension-module">
                <li v-for="(item, index) in dimensionData" @click="toggleSelectDimension(item)" :class="{'active-li': item.flag}">
                  <span>{{item.label}}</span>
                  <i class="el-icon-check" v-show="item.flag"></i>
                </li>
              </ul>
            </el-scrollbar>
          </div>

          <div class="title">度量</div>
          <div class="scroll-box2">
            <el-scrollbar style="height: 100%">
              <ul class="measure-module">
                <li v-for="(item, index) in measureData" @click="toggleSelectMeasure(item)" :class="{'active-li': item.flag}">
                  <span>{{item.label}}</span>
                  <i class="el-icon-check" v-show="item.flag"></i>
                </li>
              </ul>
            </el-scrollbar>
          </div>
        </el-col>
        <el-col :span="20">
          <div class="title">Custom</div>
          <div class="content-table">
            <ag-grid-vue style="width: 100%; height: calc(100vh - 280px);" class="ag-theme-balham"
                         :gridOptions="SampleTable"
                         :sideBar="false"
                         :enableColResize="true"
                         :enableSorting="true"
                         :enableFilter="true"
                         :groupHeaders="false"
                         :suppressRowClickSelection="true">
            </ag-grid-vue>
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
  import draggable from 'vuedraggable'
  import {AgGridVue} from "ag-grid-vue";
  export default {
    data() {
      return {
        value1: '',
        value1Options: [
          {
            value: 'CPU',
            label: 'CPU'
          },
          {
            value: 'Custom',
            label: 'Custom'
          },
        ],
        dimensionData: [
          {
            value: 'year',
            label: 'Year',
            flag: false,
            type: '',
          },
          {
            value: 'quarter',
            label: 'Quarter',
            flag: false,
            type: '',
          },
          {
            value: 'month',
            label: 'Month',
            flag: false,
            type: '',
          },
          {
            value: 'geo',
            label: 'LE Geo',
            flag: false,
            type: '',
          },

        ],
        measureData: [
          {
            value: 'CA',
            label: 'CA',
            flag: false,
            type: 'warning',
          },
          {
            value: 'Qty',
            label: 'Qty',
            flag: false,
            type: 'warning',
          },
          {
            value: 'Revenue',
            label: 'Revenue',
            flag: false,
            type: 'warning',
          },
          {
            value: 'Cost',
            label: 'Cost',
            flag: false,
            type: 'warning',
          },
        ],
        newArr: [],
        SampleData: [],
        SampleTable: {
          rowDragManaged: true, // 行拖动，配合字段中rowDrag: true
          // toolPanelSuppressRowGroups: true
        },
        tableColumn: {
          columnDefs: [
            {headerName: "Year", field: "sold_to_group"},
            {headerName: "Quarter", field: "end_customer_group"},
            {headerName: "Month", field: "sold_to"},
            {headerName: "sold_to_name", field: "sold_to_name"},
            {headerName: "sell_in_geo", field: "sell_in_geo"},
            {headerName: "sell_in_region", field: "sell_in_region"},
            {headerName: "sell_in_country", field: "sell_in_country"},
            {headerName: "sell_in_country_name", field: "sell_in_country_name"},
            {headerName: "prod_sn", field: "prod_sn"},
            {headerName: "orderid", field: "orderid"},
            {headerName: "idtype", field: "idtype"},
            {headerName: "createtime", field: "createtime"},
            {headerName: "country", field: "country"},
            {headerName: "city", field: "city"},
            {headerName: "street", field: "street"},
            {headerName: "contactphone_sc", field: "contactphone_sc"},
            {headerName: "email", field: "email"},
            {headerName: "coustomaddress_sc", field: "coustomaddress_sc"},
            {headerName: "updatetime", field: "updatetime"},
            {headerName: "closetime", field: "closetime"},
            {headerName: "updateby", field: "updateby"},
            {headerName: "orderstate_su", field: "orderstate_su"},
            {headerName: "actualservicemode_s", field: "actualservicemode_s"},
            {headerName: "zsr_wtyb", field: "zsr_wtyb"},
            {headerName: "zsr_wtye", field: "zsr_wtye"},
            {headerName: "zsrv_styp", field: "zsrv_styp"},
            {headerName: "service_geo", field: "service_geo"},
            // {headerName: "customname", field: "customname"},
            // {headerName: "sotype_s", field: "sotype_s"},

          ],
          // rowModelType: 'infinite',
          enableSorting: true,
          toolPanelSuppressRowGroups: true
        },
      }
    },
    methods: {
      toggleSelectDimension(params) {
        console.log(params,'点击的li')
        params.flag = !params.flag
        if (params.flag) {
          // 新增加的
          this.newArr.push(params)
        } else {
          // 要删除的
          let index
          for (let i in this.newArr) {
            if (this.newArr[i].label === params.label) {
              index = i
            }
          }
          this.newArr.splice(index, 1)
        }
      },
      toggleSelectMeasure(params) {
        console.log(params,'点击的li')
        params.flag = !params.flag
        if (params.flag) {
          // 新增加的
          this.newArr.push(params)
        } else {
          // 要删除的
          let index
          for (let i in this.newArr) {
            if (this.newArr[i].label === params.label) {
              index = i
            }
          }
          this.newArr.splice(index, 1)
        }
      },
      delTag(params) {
        console.log(params,'要移除的')
        params.flag = false // 和菜单栏形成联系
        // 控制拖拽组件的
        let index
        for (let i in this.newArr) {
          if (this.newArr[i].label === params.label) {
            index = i
          }
        }
        this.newArr.splice(index, 1)
      },
    },
    components: {
      draggable,
      'ag-grid-vue': AgGridVue,
    },
    watch: {
      'newArr': {
        handler: function (nVal) {
          // 监听到变化，重新set列就可以
          console.log(nVal,'的')
          let arr = nVal.map(item => {
            let fileName = ''
            for (let i in this.tableColumn.columnDefs) {
              if (item.label === this.tableColumn.columnDefs[i].headerName) {
                fileName = this.tableColumn.columnDefs[i].field
              }
            }
            return {
              headerName: item.label,
              field: fileName,
              rowDrag: true,
            }
          })
          console.log(arr,'新列')
          this.SampleTable.api.setColumnDefs(arr)
        },
        deep: true
      }
    },
    mounted() {
      let _this = this
      // Sample Data
      this.axios.get('../../../static/json/sampleData.json').then(function (res) {
        let arr = res.data.tabledate;
        _this.SampleData = arr.tabledateone;
        _this.SampleTable.api.setRowData(_this.SampleData)
        // _this.SampleTable.api.setPinnedTopRowData('好') 设置固定行
        _this.SampleTable.api.setColumnDefs(_this.tableColumn.columnDefs)
        // _this.SampleTable.api.sizeColumnsToFit()
      })
    }
  }
</script>

<style lang="scss" scoped>
  $borderColor: #666;
  $borderColor2: #b3b3b3;
  .demo1 {
    position: relative;
    padding: 20px;
    color: $borderColor;
    .dragDrop-module {
      border: 1px solid $borderColor2;
      min-height: 32px;
      position: relative;
      padding: 5px;
      .el-tag {
        margin-right: 5px;
      }
    }
    .main {
      .scroll-box {
        border: 1px solid $borderColor2;
        height: 50vh;
      }
      .scroll-box2 {
        height: 30vh;
        border: 1px solid $borderColor2;
      }
      .dimension-module, .measure-module {
        li {
          position: relative;
          list-style: none;
          height: 30px;
          line-height: 30px;
          padding: 10px;
          border-bottom: 1px solid #e5e5e5;
          cursor: pointer;
          user-select: none;
          &:hover {
            background-color: #f2f2f2;
          }
          i {
            position: absolute;
            right: 10px;
            top: 15px;
            font-size: 20px;
            font-weight: bold;
          }
        }
        .active-li {
          background-color: #52cc52!important;
          color: #fff!important;
        }
      }
    }
    .title {
      font-weight: bold;
      font-size: 16px;
      margin: 5px 0;
    }
  }
</style>
<style lang="scss">
  .demo1 {
    .main {
      .el-scrollbar__wrap {
        overflow-x: hidden;
      }
    }
  }
</style>
