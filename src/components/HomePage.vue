<template>
  <div class='HomePage'>
    <p class='title'>电力变压器在线故障检测系统</p>
    <p class='list'>
      <span>文本(F)</span>
      <span>编辑(E)</span>
      <span>查看(V)</span>
      <span>帮助(H)</span>
      <span>图像处理(D)</span>
      <span>图像统计(S)</span>
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
        <p class='item'>系统设置</p>
        <p class='item'>检测设置</p>
        <p class='item'>历史数据查询</p>
        <p class='item'>报警记录</p>
        <p class='item'>故障分析报告</p>
        <div class='item' style='position: relative;'>图像采集周期
          <p class='item-right'>
            <span>|</span><span class='item-time'>分钟</span><span class='icon-arrow'></span>
          </p>
        </div>
        <p class='item'>基准热图选择</p>
      </div>
      <div class='right'>
        <div class='img-wrapper'>
          <img src="../assets/1.jpg" alt="" style='margin-right:145px;'>
          <img src="../assets/2.jpg" alt="">
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
            <span class='icon-chachepanzhishideng light' style='color:#97E304;'></span>
            系统状态
          </div>
          <div class='light-group'>
            <span class='icon-chachepanzhishideng light' style='color:#97E304;'></span>
            自动检测
          </div>
          <div class='light-group'>
            <span class='icon-chachepanzhishideng light' style='color:#97E304;'></span>
            热像仪连接
          </div>
          <div class='light-group'>
            <span class='icon-chachepanzhishideng light' style='color:red;'></span>
            报警
          </div>
          <div class='tip'>
            <p>说明</p>
            <p>启动自动检测......</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
// TODO:引入elementUi的select和table
export default {
  name: 'Home',
  data () {
    return {
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
      ]
    }
  }
}
</script>

<style scoped lang='less'>
.HomePage{
  height: 100%;
  .title{
    text-align: center;
    margin-top:16px;
  }
  .list{
    overflow: hidden;
    padding:15px 30px;
    span{
      float: left;
      margin-right:32px;
      cursor: pointer;
    }
  }
  .banner{
    height: 150px;
    line-height: 150px;
    background:#bfbfbf;
    text-align:center;
    font-size: 40px;
  }
  .main{
    overflow: hidden;
    margin-top:50px;
    margin-bottom:50px;
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
          width:80px;
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
      height:690px;
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
