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
            <draggable v-model="dragDropData" element="div">
              <el-tag
              v-for="tag in dragDropData"
              :key="tag.label"
              :closable="true"
              @close="delTag(tag)"
              :type="tag.type">
              {{tag.label}}
              </el-tag>
            </draggable>
            <!--<el-tag-->
              <!--v-for="tag in dragDropData"-->
              <!--:key="tag.label"-->
              <!--:closable="true"-->
              <!--@close="delTag(tag)"-->
              <!--:type="tag.type">-->
              <!--{{tag.label}}-->
            <!--</el-tag>-->
            <!--{{dragDropData}}-->
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
  import draggable from 'vuedraggable'
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
      delTag(params) {
        console.log(params,'要移除的')
        params.flag = false
      },
    },
    computed: {
      // dragDropData: function () {
      //   let newArr = []
      //   for(let i in this.dimensionData) {
      //     if (this.dimensionData[i].flag === true) {
      //       newArr.push(this.dimensionData[i])
      //     }
      //   }
      //   for(let i in this.measureData) {
      //     if (this.measureData[i].flag === true) {
      //       newArr.push(this.measureData[i])
      //     }
      //   }
      //   return newArr
      // },
      dragDropData: {
        get: function () {
          let newArr = []
          for(let i in this.dimensionData) {
            if (this.dimensionData[i].flag === true) {
              newArr.push(this.dimensionData[i])
            }
          }
          for(let i in this.measureData) {
            if (this.measureData[i].flag === true) {
              newArr.push(this.measureData[i])
            }
          }
          return newArr
        },
        set: function (newValue) {
          console.log(newValue,'狂顶狂顶')
          // this.dragDropData = newValue
          // this.dimensionData = newValue
        }
      }
    },
    components: {
      draggable,
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
      position: relative;
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
