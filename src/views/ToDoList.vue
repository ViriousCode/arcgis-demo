<template>
  <div>
    <!-- <div id="move-ball-one" class="move-ball">
      <i class="el-icon-cold-drink"></i>
    </div> -->
    <div class="flex">
      <el-card class="to-do-list-card" shadow="hover" v-for="item in cardData" :key="item.title">
        <template #header>
          <div class="card-header">
            <div class="col-center">
              {{item.title}}
              <i class="el-icon-caret-bottom"></i>
            </div>
            <el-button type="primary" @click="addCount(item)">详情</el-button>
          </div>
        </template>
        <el-drawer v-model="item.cardDetailVisible" direction="ltr" modal-class="drawer-modal-class">
          <el-row gutter="5%">
            <el-col :span="24">
              <span>{{item.target}}</span>
            </el-col>
            <el-col :span="24">
              <el-date-picker value-format="YYYY-MM-DD" @change="dateChange" v-model="item.datePickerData"
                type="daterange" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期">
              </el-date-picker>
            </el-col>
            <el-col :span="24">
              <span>{{item.target}}</span>
            </el-col>
          </el-row>
          <el-button type="primary" @click="onSaveBtnClick(item)">保存</el-button>
        </el-drawer>
      </el-card>
      <div class="to-do-list-card child-center border-1">
        <div class="add-icon"></div>
      </div>
    </div>
    <!-- <div class="flex">
      <div class="run-ball" style="width: 100%;height: 500px;background: rgb(180, 178, 178);position: relative;">000
      </div>
    </div> -->
    <!-- <a></a> -->
  </div>
</template>
<script lang="ts">
  import { defineComponent, reactive, toRefs,onMounted } from 'vue'
  export default defineComponent({
    setup() {
      const data = reactive({
        cardData: [
          {
            title: 'card1',
            count: 0,
            cardDetailVisible: false,
            target: 'aaaa',
            datePickerData: ''
          },
          {
            title: 'card2',
            count: 0,
            cardDetailVisible: false,
            datePickerData: ''
          }
        ]
      })
      const addCount = function (item: any) {
        // console.log(item)
        item.count++
        // item.cardDetailVisible = true
      }
      const changeTitle = function () {
        data.cardData[1].title = 'ca'
      }
      const dateChange = function (date: any) {
        // console.log(date,date[1],date[2])
      }
      const onSaveBtnClick = function (item: any) {
        // console.log(item)
        localStorage.setItem(item.title, JSON.stringify(item))
        const getItem = JSON.parse(localStorage.getItem(item.title) + "")
        console.log('wwwwwwwwww', getItem)
        // console.log(JSON.parse('{"title":"card1","count":1,"cardDetailVisible":true,"target":"aaaa","datePickerData":["2022-03-04","2022-04-12"]}'))
      }
      // setTimeout(()=>{
      //   changeTitle()
      // }, 1000)
      const toRefsData = toRefs(data)
      onMounted(()=>{
        const moveBallOne = document.getElementById('move-ball-one') as HTMLElement
        document.addEventListener('click', function(e){
          moveBallOne.style.transform = 'translateY(' + (e.clientY - 50) + 'px)'
          moveBallOne.style.transform += 'translateX(' + (e.clientX - 50) + 'px)'
        })
        const aaa = function() {
          console.log('mousemove')
        }
      })
      return {
        ...toRefsData,
        addCount,
        dateChange,
        onSaveBtnClick
      }
    }
  })
</script>
<style lang="scss" scoped>
  .to-do-list-card {
    width: 240px;
    margin: 5px;
    height: 320px;
  }

  .run-ball:before {
    width: 20%;
    height: 20%;
    /* background: url('../assets/img/6.jpg'); */
    background-size: contain;
    background-repeat: no-repeat;
    z-index: 1111;
    position: absolute;
    content: '';
    margin: 0 0 0 -36%;
  }

  .run-ball:hover:before {
    animation-duration: 10s;
    animation-name: runcycle;
    /* 循环次数 infinite无限循环*/
    animation-iteration-count: infinite;
    /* 反着再播一遍 */
    animation-direction: alternate;
  }

  @keyframes runcycle {
    from {
      margin: 0 0 0 -36%;
    }

    25% {
      margin: 0 0 0 44%;
      filter: drop-shadow(16px 16px 20px rgb(245, 255, 110)) invert(75%);
    }

    50% {
      margin: 50% 0 0 44%;
      filter: drop-shadow(16px 16px 20px rgb(177, 255, 249)) invert(5%);
    }

    75% {
      margin: 50% 0 0 -36%;
      filter: drop-shadow(16px 16px 20px rgb(255, 170, 244)) invert(75%);
    }

    to {
      margin: 0 0 0 -36%;
      filter: drop-shadow(16px 16px 20px rgb(139, 255, 145)) invert(5%);
    }
  }

  .col-center {
    margin: auto 0;
  }

  .row-center {
    margin: 0 auto;
  }

  .drawer-modal-class {
    background: aqua;
  }

  .card-header {
    display: flex;
    justify-content: space-between;
  }

  .child-center {
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .border-1 {
    border: 1px solid #000;
  }

  .move-ball{
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: #58c2ff;
    z-index: 111;
    /* 脱离文档流 */
    position: fixed;
    transition: 1s;
  }

  /* .add-icon{

  } */
  .add-icon {
    /* position: absolute; */
    width: 60px;
    height: 60px;
    background: #58c2ff;
    -webkit-transform: translate(0, 0) rotate(0deg);
    transform: translate(0, 0) rotate(0deg);
    border-radius: 50%;
    cursor: pointer;
    z-index: 100;
    /* -webkit-transition: 0.4s cubic-bezier(0.2, 0.6, 0.3, 1.1); */
    /* transition: 0.4s cubic-bezier(0.2, 0.6, 0.3, 1.1); */
  }

  /* .add-icon:after {
content: '';
position: absolute;
top: 50%;
left: 50%;
-webkit-transform: translate(-50%, -50%);
transform: translate(-50%, -50%);
height: 2px;
width: 50%;
background: white;
}
.add-icon:before {
content: '';
position: absolute;
top: 50%;
left: 50%;
-webkit-transform: translate(-50%, -50%);
transform: translate(-50%, -50%);
height: 50%;
width: 2px;
background: white;
}

.add-icon.clicked {
-webkit-transform: translate(-50%, -50%) rotate(360deg);
transform: translate(-50%, -50%) rotate(360deg);
background: #CC2A41;
}

.add-icon.clicked:before {
width: 0;
} */

  .flex {
    display: flex;
  }

  * {
    margin: 0;
    padding: 0;
  }

  body {
    background-color: #000;
  }

  a {
    text-decoration: none;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    font-size: 24px;
    background: linear-gradient(90deg, #03a9f4, #f441a5, #03a9f4);
    background-size: 400%;
    width: 400px;
    height: 100px;
    color: white;
    text-align: center;
    line-height: 100px;
    text-transform: uppercase;
    border-radius: 50px;
  }

  a:hover::before {
    animation: sun 8s infinite;
  }

  a::before {
    content: "";
    position: absolute;
    left: -5px;
    right: -5px;
    top: -5px;
    bottom: -5px;
    /* border: 1px solid red; */
    background: linear-gradient(90deg, #03a9f4, #f441a5, #03a9f4);
    background-size: 400%;
    border-radius: 50px;
    filter: blur(20px);
    z-index: -1;
  }

  @keyframes sun {
    100% {
      background-position: -400% 0;
    }
  }
</style>