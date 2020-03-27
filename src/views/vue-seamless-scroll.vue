<template>
  <div class="container">
    <div class="container_sideBar">
      <div class="sideBar_t">
        <el-carousel :interval="5000" indicator-position="none" height="100%" style="height: 100%">
          <el-carousel-item v-for="item in taskList" :key="item.id">
            <div :style="{ background: item.bg, height: '100%'}">
              <span>{{ item.station_name }}</span> |
              <span>{{ item.progressNum }}</span> |
              <span>{{ item.times }}</span>
            </div>
          </el-carousel-item>
        </el-carousel>
      </div>
      <div class="sideBar_b">
        <div class="seamless-warp scroll_con" style="height: 100%">
          <ul id="swiper">
            <li v-for="item in taskList" :key="item.id" class="item" style="height: 25%">
              <span class="left-border">{{ item.id }}</span>
              <span class="income-title">{{ item.station_name }}</span>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="container_main">container-r
      <div class="items item_lt">{{ findData }}</div>
      <div class="items item_rt">{{ findData }}</div>
      <div class="items item_lb">{{ findData }}</div>
      <div class="items item_rb">{{ findData }}</div>
      <div class="items item_center">
        <ul>
          <li v-for="(item, index) in highlightData" :key="index" :class="{ isActive : active == index }">{{ item }} {{ index }}</li>
        </ul>
      </div>
    </div>
    <!-- <div class="seamless-warp scroll_con">
      <ul id="swiper">
        <li v-for="item in taskList" :key="item.id" class="item" style="height: 20%">
          <span class="left-border">{{ item.id }}</span>
          <span class="income-title">{{ item.station_name }}</span>
        </li>
      </ul>
    </div>
    <el-carousel :interval="5000" direction="vertical" indicator-position="none" height="400px" style="flex: 1">
      <el-carousel-item v-for="item in taskList" :key="item.id">
        <div :style="{ background: item.bg, height: '100%'}">
          <span>{{ item.station_name }}</span> |
          <span>{{ item.progressNum }}</span> |
          <span>{{ item.times }}</span>
        </div>
      </el-carousel-item>
    </el-carousel>-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeChartIndex: 0,
      taskList: [
        {
          id: 0,
          bg: "#ccc",
          station_name: "beijing",
          progressNum: 70,
          teamsNum: 300,
          targetsNum: 600,
          times: "5/20 9:20~5/20 18:20"
        },
        {
          id: 1,
          bg: "red",
          station_name: "shanghai",
          progressNum: 50,
          teamsNum: 20,
          targetsNum: 8,
          times: "5/21 9:20~5/21 18:20"
        },
        {
          id: 2,
          bg: "#eee",
          station_name: "shijiazhuang",
          progressNum: 80,
          teamsNum: 10,
          targetsNum: 10,
          times: "5/22 9:20~5/22 18:20"
        },
        {
          id: 3,
          bg: "green",
          station_name: "guangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 4,
          bg: "blue",
          station_name: "shenzhen",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 5,
          bg: "yellow",
          station_name: "tianjing",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 6,
          bg: "black",
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 7,
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 8,
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 9,
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 10,
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        },
        {
          id: 11,
          station_name: "hangzhou",
          progressNum: 30,
          teamsNum: 50,
          targetsNum: 4,
          times: "5/23 9:20~5/23 18:20"
        }
      ],
      findData: {},
      // 高亮data
      highlightData: [
        { id: 0, name: '123456', age: 18},
        { id: 1, name: 'sfdsfw', age: 20},
        { id: 2, name: 'dffdvf', age: 22},
        { id: 3, name: 'sdgsge', age: 21},
      ],
      active: 3
    }
  },
  methods: {
    moveTimer() {
      this.$nextTick(() => {
        setInterval(() => {
          this.move();
        }, 5000);
      });
    },
    // 高亮定时器
    highlightTimer() {
      this.$nextTick(() => {
        setInterval(() => {
          this.highlightMove();
        }, 2000);
      });
    },
    highlightMove() {
      this.active--
      console.log(this.active)
      if (this.active === -1) this.active = 3
      // if (this.active === this.highlightData.length) this.active = 3
    },
    // 数据滚动
    move() {
      // let swiper = this.$refs.swiper
      let swiper = document.querySelector("#swiper");
      let scroll_con = document.querySelector(".scroll_con");
      let item = document.querySelector(".item");
      this.activeChartIndex++;
      this.findDataFun(this.activeChartIndex)
      // console.log(scroll_con.style.height);
      // 每条数据的高度
      let item_h = Number(item.style.height.slice(0, 2));
      // let item_h = (Number(item.style.height.slice(0, 2)) / 100) * 400 + 20; // 重新计算值
      let scroll_con_h = Number(scroll_con.style.height.slice(0, 3));
      // console.log(item_h);
      if (this.taskList.length * item_h > scroll_con_h) {
        swiper.style.transform = `translate3d(0, -${ this.activeChartIndex * item_h }%, 0)` // 向上移动百分比
        swiper.style.transition = "transform 2s"
      }

      if (this.activeChartIndex === this.taskList.length) {
        this.activeChartIndex = 0
        this.animating = true
        clearTimeout(this.transitionTimer)
        this.transitionTimer = setTimeout(() => {
          swiper.style.transform = "translate3d(0%, 0, 0)"
          swiper.style.transition = ""
          this.animating = false
        }, 2000)
      }
    },
    findDataFun(index) {
      // console.log(index)
      this.findData = this.taskList.find((item, ind) => {
        return index === ind
      })
      if (this.findData === undefined) this.findData = this.taskList[0]
    }
  },
  mounted() {
    this.findDataFun(0)
    this.moveTimer()
    this.highlightTimer()
  }
}
</script>

<style lang="less">
.isActive {
  background-color: chartreuse;
  border: 1px solid aquamarine !important;
}
.container {
  height: 100%;
  min-width: 1200px;
  min-height: 768px;
  overflow: hidden;
  background-color: aquamarine;
  display: flex;
  .container_sideBar {
    width: 25%;
    background-color: cadetblue;
    .sideBar_t {
      height: 40%;
      background-color: antiquewhite;
    }
    .sideBar_b {
      height: 60%;
      background-color: #ccc;
    }
  }
  .container_main {
    width: 75%;
    position: relative;
    background-color: darkgoldenrod;
    .items {
      position: absolute;
      width: 30%;
      height: 30%;
    }
    .item_lt {
      left: 0;
      top: 0;
      background-color: aqua;
      // transform: translate3d(60%, 0, 0);
      // transition: transform 2s;
    }
    .item_rt {
      right: 0;
      top: 0;
    }
    .item_lb {
      left: 0;
      bottom: 0;
    }
    .item_rb {
      bottom: 0;
      right: 0;
      background-color: aquamarine;
    }
    .item_center {
      height: 60%;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      background-color: cadetblue;
      ul {
        height: 100%;
        margin: 0;
        padding: 0;
        li {
          height: 25%;
          list-style: none;
          box-sizing: border-box;
          border: 1px solid #cccccc;
        }
      }
    }
  }
}
.seamless-warp {
  overflow: hidden;
  ul {
    height: 100%;
    margin: 0;
    padding: 0;
    li {
      background: violet;
      box-sizing: border-box;
      border-top: 1px solid green;
      height: 10%;
      list-style: none;
    }
  }
}
</style>
