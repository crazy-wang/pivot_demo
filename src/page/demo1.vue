<template>
  <div class="demo1">
    <div class="header">
      <el-row :gutter="20">
        <el-col :span="4">
          <div class="select-module">
            <div class="title">选择可视化表</div>
            <el-select v-model="value1" placeholder="请选择">
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
          <div class="title">度量</div>
          <div class="content-table">
           AG-GRID表格
          </div>
        </el-col>
      </el-row>
    </div>
  </div>
</template>

<script>
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
          },
          {
            value: 'quarter',
            label: 'Quarter',
            flag: false,
          },
          {
            value: 'month',
            label: 'Month',
            flag: false,
          },
          {
            value: 'geo',
            label: 'LE Geo',
            flag: false,
          },

          {
            value: 'year',
            label: 'Year',
            flag: false,
          },
          {
            value: 'quarter',
            label: 'Quarter',
            flag: false,
          },
          {
            value: 'month',
            label: 'Month',
            flag: false,
          },
          {
            value: 'geo',
            label: 'LE Geo',
            flag: false,
          },
          {
            value: 'year',
            label: 'Year',
            flag: false,
          },
          {
            value: 'quarter',
            label: 'Quarter',
            flag: false,
          },
          {
            value: 'month',
            label: 'Month',
            flag: false,
          },
          {
            value: 'geo',
            label: 'LE Geo',
            flag: false,
          },
        ],
        measureData: [
          {
            value: 'CA',
            label: 'CA',
            flag: false,
          },
          {
            value: 'Qty',
            label: 'Qty',
            flag: false,
          },
          {
            value: 'Revenue',
            label: 'Revenue',
            flag: false,
          },
          {
            value: 'Cost',
            label: 'Cost',
            flag: false,
          },
        ],
      }
    },
    methods: {
      toggleSelectDimension(params) {
        console.log(params,'点击的li')
        params.flag = !params.flag
      },
      toggleSelectMeasure(params) {
        console.log(params,'点击的li')
        params.flag = !params.flag
      },
    }
  }
</script>

<style lang="scss" scoped>
  $borderColor: #666;
  .demo1 {
    position: relative;
    padding: 20px;
    color: $borderColor;
    .dragDrop-module {
      border: 1px solid $borderColor;
      min-height: 40px;
    }
    .main {
      .scroll-box {
        border: 1px solid $borderColor;
        height: 50vh;
      }
      .scroll-box2 {
        height: 30vh;
        border: 1px solid $borderColor;
      }
      .dimension-module, .measure-module {
        li {
          position: relative;
          list-style: none;
          height: 30px;
          line-height: 30px;
          padding: 10px;
          border-bottom: 1px solid $borderColor;
          cursor: pointer;
          user-select: none;
          i {
            position: absolute;
            right: 10px;
            top: 15px;
            font-size: 20px;
            font-weight: bold;
          }
        }
        .active-li {
          background-color: #52cc52;
          color: #fff;
        }
      }
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
