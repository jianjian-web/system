<template>
  <div class='HomePage'>
    <!-- <p class='title'>电力变压器在线故障检测系统</p> -->
    <p class='list'>
      <span>
        文本(F)
      </span>
      <span>编辑(E)</span>
      <span>查看(V)</span>
      <span>帮助(H)</span>
      <span>
        <el-dropdown trigger="click">
          <span class="el-dropdown-link">
            图像处理(D)
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>线性变换</el-dropdown-item>
            <el-dropdown-item>阙值变换</el-dropdown-item>
            <el-dropdown-item>灰度拉伸</el-dropdown-item>
            <el-dropdown-item>中值滤波</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </span>
      <span>
        <el-dropdown trigger="click">
          <span class="el-dropdown-link">
            图像统计(S)
          </span>
          <el-dropdown-menu slot="dropdown">
            <el-dropdown-item>绘制直方图</el-dropdown-item>
          </el-dropdown-menu>
        </el-dropdown>
      </span>
    </p>
    <p class='banner'>
      电力变压器在线故障检测系统
    </p>
    <div class='main content'>
      <div class='left'>
        <div class='form'>
          <p class='form-title'>
            管理员登录
          </p>
          <div class='form-body'>
            <input type="text" class='input' placeholder="用户名">
            <input style='margin-top:18px;' type="text" class='input' placeholder="密码">
            <p class='btnGroup'>
              <span class='btn' style='margin-right:15px;'>登录</span>
              <span class='btn'>退出</span>
            </p>
          </div>
        </div>
        <p class='item' @click='system = true'>系统设置</p>
        <p class='item' @click='monitor = true'>检测设置</p>
        <p class='item'>历史数据查询</p>
        <p class='item' @click='danger = true'>报警记录</p>
        <p class='item'>故障分析报告</p>
        <div class='item' style='position: relative;'>图像采集周期
          <p class='item-right'>
            <el-select v-model="selectValue" placeholder="请选择" style='border:none;padding:0;'>
              <el-option label="1分钟" value="1分钟"></el-option>
              <el-option label="5分钟" value="5分钟"></el-option>
              <el-option label="10分钟" value="10分钟"></el-option>
              <el-option label="30分钟" value="30分钟"></el-option>
              <el-option label="1小时" value="1小时"></el-option>
            </el-select>
          </p>
        </div>
        <p class='item'>基准热图选择</p>
      </div>
      <div class='right'>
        <div class='img-wrapper'>
          <div>
            <img src="../assets/img.jpg" alt="" style='width:410px;margin-right:10px;'>
            <span>
              当前热图
            </span>
          </div>
          <div>
            <img src="../assets/img.jpg" alt="" style='width:410px;'>
            <span>
              基准热图
            </span>
          </div>
        </div>
        <p class='table-title'>检测区数据显示</p>
        <p style='text-align:right'>当前日期：{{new Date().getFullYear()}}年{{new Date().getMonth()+1}}月{{new Date().getDate()}}日</p>
        <div class='form-wrapper'>
          <el-table
              border
              :data="tableData"
              style="width: 100%">
              <el-table-column
                prop="name"
                align='center'
                >
              </el-table-column>
              <el-table-column
                prop="tem"
                label="当前温度"
                align='center'
                >
              </el-table-column>
              <el-table-column
                prop="max"
                align='center'
                label="历史最高温度">
              </el-table-column>
              <el-table-column
                prop="ave"
                align='center'
                label="区域平均温度">
              </el-table-column>
          </el-table>
          <div class='form-td'>
            <span class='title1'>溫度</span>
            <span class='title2'>部位</span>
            <span class='line'></span>
          </div>
        </div>
        <p class='table-title' style='margin-top:29px;'>系统状态</p>
        <div class='light-wrapper'>
          <div class='light-group'>
            <span class='myicon-chachepanzhishideng light' style='color:#97E304;'></span>
            系统状态
          </div>
          <div class='light-group'>
            <span class='myicon-chachepanzhishideng light' style='color:#97E304;'></span>
            自动检测
          </div>
          <div class='light-group'>
            <span class='myicon-chachepanzhishideng light' style='color:#97E304;'></span>
            热像仪连接
          </div>
          <div class='light-group'>
            <span class='myicon-chachepanzhishideng light' style='color:red;'></span>
            报警
          </div>
          <div class='tip'>
            <p>说明</p>
            <p>启动自动检测......</p>
          </div>
        </div>
      </div>
    </div>
    <el-dialog
      :visible.sync="system"
      width="645px"
      >
      <div class='system-body'>
        <p class='dialog-title'>系统设置</p>
        <div class='dialog-content'>
          <div class='tree-menu'>
            <el-tree :data="data" :props="defaultProps" :default-expanded-keys="[1]" node-key="id"></el-tree>
          </div>
          <div class='dialog-setting'>
            <p>报警温度设置</p>
            <p class='btn-group'>
              <span :class='{active: current === 0}' @click='current = 0'>
                A (变压器箱体) 
              </span>
              <span :class='{active: current === 1}' @click='current = 1'>
                B (油枕) 
              </span>
              <span :class='{active: current === 2}' @click='current = 2'>
                C (套管) 
              </span>
            </p>
            <div class='input-group'>
               <p>绝对温度判断报警法</p>
               <p>
                 <label>请输入正常工作时的最高温度</label><input value='60' type="text" style='float:right;padding:5px;width:160px;border:none;background:#F8F8F8;'>
               </p>
               <p>
                 <label>请输入产生严重故障的最低温度</label><input value='75' type="text" style='float:right;padding:5px;width:160px;border:none;background:#F8F8F8;'>
               </p>
            </div>
            <div class='input-group' style='height:145px;'>
               <p>相对温度判断报警法</p>
               <p>
                 <label>请输入正常工作时的温度</label><input value='50' type="text" style='float:right;padding:5px;width:160px;border:none;background:#F8F8F8;'>
               </p>
               <p>
                 <label>请输入正常工作时的环境温度</label><input value='27' type="text" style='float:right;padding:5px;width:160px;border:none;background:#F8F8F8;'>
               </p>
                <p>
                 <label>请输入与参考图像的最大温差</label><input value='20' type="text" style='float:right;padding:5px;width:160px;border:none;background:#F8F8F8;'>
               </p>
            </div>
          </div>
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="system = false">取 消</el-button>
        <el-button type="primary" @click="system = false">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog
      :visible.sync="danger"
      width="645px"
      >
      <div class='system-body'>
        <p class='dialog-title'>警告</p>
        <div class='dialog-content'>
          <div style='flex:1;display:flex;'>
            <div style='padding-top:40px'>
              <img src="../assets/dange.png" alt="">
            </div>
            <div style='flex:1;margin-left:40px;display:flex;flex-direction: column;justify-content: space-between;'>
              <p>监测点</p>
              <p>报警原因</p>
              <p>报警依据</p>
              <p>监测点正常工作最高温度阙值</p>
              <p>监测点当前温度</p>
              <p>超过报警温度阙值</p>
              <p>建议采取的措施</p>
            </div>
          </div>
          <div style='flex:1'>
            <div style='flex:1;margin-left:40px;display:flex;flex-direction: column;justify-content: space-between;height:100%;'>
              <p>C(套管）存在一般热缺陷</p>
              <p>监测点温度超过正常工作的最高温度</p>
              <p>绝对温度判断法</p>
              <p>53.3°C(2017.5.18-19:43:15)</p>
              <p>52.2ºC</p>
              <p>3.3ºC</p>
              <p>应引起注意，寻找机会处理</p>
            </div>
          </div>
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="danger = false">取 消</el-button>
        <el-button type="primary" @click="danger = false">确 定</el-button>
      </span>
    </el-dialog>
    <el-dialog
      :visible.sync="monitor"
      width="645px"
      >
      <div class='system-body'>
        <p class='dialog-title'>监测方式设置</p>
        <div class='dialog-content' style='flex-direction: column;justify-content: space-around;'>
          <el-checkbox v-model="checked">定时监测</el-checkbox><br/>
          <div style='flex:1;height:86px;background:#fff;line-height:86px;padding-left:25px;' class='wrapper'>
            <label>监测周期</label>
            <el-select v-model="selectValue2" placeholder="请选择" style='border:none;padding:0;margin-left:20px;'>
              <el-option label="1小时" value="1小时"></el-option>
              <el-option label="2小时" value="2小时"></el-option>
              <el-option label="3小时" value="3小时"></el-option>
            </el-select>
          </div>
          <el-checkbox v-model="checked2" style='margin-top:20px;'>整点监测</el-checkbox><br/>
          <div style='flex:2;height:86px;background:#fff;display:flex;flex-wrap: wrap;'>
            <el-checkbox style='flex:1 1 16.6%;margin-left:30px;' v-model="checked4[item]" v-for='item in 24' :key='item'>{{item}}点</el-checkbox>
          </div>
        </div>
      </div>
      <span slot="footer" class="dialog-footer">
        <el-button @click="monitor = false">取 消</el-button>
        <el-button type="primary" @click="monitor = false">确 定</el-button>
      </span>
    </el-dialog>
  </div>
</template>

<script>
// TODO:引入elementUi的select和table
export default {
  name: 'Home',
  data () {
    return {
      checked: false,
      checked2: false,
      checked4: [],
      monitor: false,
      selectValue: '1分钟',
      selectValue2: '1小时',
      current: 0,
      danger: false,
      system: false,
      tableData: [
        {
          name: '变压器箱体 (A)',
          tem: '50.3℃',
          max: '50.8℃',
          ave: '45.9℃'
        },
        {
          name: '变压器套管 (B)',
          tem: '48.9℃',
          max: '50.1℃',
          ave: '41.8℃'
        },
        {
          name: '变压器油机 (C)',
          tem: '40.1℃',
          max: '43.8℃',
          ave: '36.1℃'
        }
      ],
      data: [{
          label: '在线监测',
          id:1,
          children: [{
            label: '图像设置'
          },
          {
            label: '网络设置'
          },
          {
            label: '报警设置'
          }]
        }, {
          label: '数据分析',
          children: [{
            label: '数据1'
          }, {
            label: '数据2'
          }]
        }],
        defaultProps: {
          children: 'children',
          label: 'label'
        }
    }
  }
}
</script>

<style scoped lang='less'>
.HomePage{
  height: 100%;
  .system-body{
    // border:1px solid red;
    height:450px;
    margin:-50px -20px -10px -20px;
    background:#F2F2F2;
    .dialog-title{
      height:50px;
      line-height: 50px;
      background:#fff;
      text-align:center;
      font-size:16px;
      font-weight: bold;
      border-bottom:1px solid #dadada;
    }
    .dialog-content{
      padding:20px 40px;
      height:calc(~'100% - 50px');
      display: flex;
      .active{
        background:#C8997F!important;
        color:#fff;
      }
      .tree-menu{
        height:100%;
        width:169px;
        border:1px solid #dadada;
        background:#fff;
        border-radius: 5px;
      }
      .dialog-setting{
        margin-left:12px;
        flex:1;
        // border:1px solid red;
        .btn-group{
          margin-top:15px;
          span{
            cursor: pointer;
            padding:10px 20px;
            background:#fff;
            margin-right:10px;
            border-radius: 5px;
            border:1px solid #DADADA;
            &:hover{
              background:#C8997F;
              color:#fff;
            }
          }
        }
        .input-group{
          margin-top:15px;
          border:1px solid #DADADA;
          background:#fff;
          height:120px;
          display: flex;
          flex-direction: column;
          justify-content: space-around;
          padding:0 10px;
        }
      }
    }
  }
  .title{
    text-align: center;
    margin-top:16px;
  }
  .list{
    overflow: hidden;
    padding:15px 30px;
    &>span{
      float: left;
      // margin-right:32px;
      padding:8px 14px;
      cursor: pointer;
      border:1px solid #d0d0d0;
      border-left:none;
      &:hover{
        background:#aaa;
        color:#fff!important;
      }
    }
     &>span:nth-child(1){
      border-left:1px solid #d0d0d0;
    }
  }
  .banner{
    height: 150px;
    line-height: 150px;
    // background:#bfbfbf;
    text-align:center;
    font-size: 40px;
    font-weight: blod;
    color:#fff;
    background: url('../assets/bg.png') no-repeat center;
  }
  .main{
    overflow: hidden;
    margin-top:50px;
    margin-bottom:20px;
    .form{
      background:#f3f3f3;
      height:260px;
      border: 1px solid #c4c4c4;
      margin-bottom: 35px;
      .form-title{
        background:#e9e9e9;
        height: 60px;
        line-height: 60px;
        text-align: center;
        font-size: 18px;
        border-bottom:1px solid #c4c4c4;
      }
      .form-body{
        padding:29px 44px;
        .input{
          width:100%;
          height:39px;
          border: 1px solid #c4c4c4;
          padding-left:10px;
        }
        .btnGroup{
          margin-top:9px;
          .btn{
            display: inline-block;
            width:102px;
            border:1px solid #c4c4c4;
            height:37px;
            text-align:center;
            line-height: 37px;
            background:#fff;
            cursor: pointer;
          }
        }
      }
    }
    .left{
      float: left;
      width:313px;
      margin-right:53px;
      height:690px;
      .item{
        text-align: center;
        height: 42px;
        line-height: 42px;
        background-color: #f3f3f3;
        border: solid 1px #c4c4c4;
        margin-bottom:15px;
        cursor: pointer;
        .item-right{
          float: right;
          width:90px;
          // border:1px solid red;
          right: 0;
          top:0;
          bottom:0;
          position: absolute;
          line-height: 42px;
          .icon-arrow{
            border:6px solid transparent;
            border-top-color:#444;
            position: relative;
            top:12px;
          }
          .item-time{
            margin: 0 10px;
          }
        }
      }
    }
    .right{
      // border:1px solid blue;
      height:720px;
      float: right;
      width:830px;
      .img-wrapper{
        display: flex;
      }
      .table-title{
        margin-top:40px;
        font-size:18px;
        color:#444;
        text-align:center;
      }
      .tip{
        border:1px solid #C4C4C4;
        flex:1;
        padding:10px;
        color:#666;
      }
      .light-wrapper{
        display: flex;
        margin-top:22px;
        .light-group{
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          width:84px;
          text-align:center;
          height:70px;
          margin-right:70px;
          background:#F3F3F3;
          border:1px solid #C4C4C4;
        }

        .light{
          font-size: 30px;
          margin-bottom:5px;
          // margin-right:70px;
        }
      }
      .form-wrapper{
        // border:1px solid red;
        position: relative;
        margin-top:15px;
        .form-td{
          position: absolute;
          top:0;
          left:0;
          height:48px;
          width:207px;
          .title1{
            position: absolute;
            right:5px;
            top:10px;
            color:#909399;
            font-weight: bold;
          }
          .title2{
            position: absolute;
            left:15px;
            bottom:10px;
            color:#909399;
            font-weight: bold;
          }
          .line{
            position: absolute;
            width:213px;
            height: 1px;
            background:#EBEEF5;
            transform: rotate(13deg);
            transform-origin: 0 0;
          }
        }
      }
    }
  }
}
</style>
