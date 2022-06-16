<template>
  <div class="github-wall">
    <div class="total">
      <span>{{ testSum.length }} contributions in this year</span>
    </div>
    <svg width="880px" height="130px">
      <g transform="translate(15, 20)">
        <!-- week -->
        <g
          :transform="`translate(${index * 16}, 0)`"
          v-for="(item, index) in 53"
          :key="index"
        >
          <!-- day -->
          <rect
            v-for="(d, i) in groupDate[index]"
            :key="i"
            width="11"
            class="day-rect"
            :title="d"
            height="11"
            x="16"
            :y="i * 15"
            rx="2"
            ry="2"
            :fill="convertFill(d)"
            :style="`
            ${
              convertFill(d) !== '#282d34'
                ? 'outline: 1px solid rgba(255, 255, 255, 0.05);outline-offset: -1px;'
                : ''
            }
              `"
          >
            <title>{{ convertText(d) }}</title>
          </rect>
        </g>
        <!-- week -->
        <g
          :transform="`translate(-30, 0)`"
          v-for="(item, index) in 1"
          :key="`g${index}`"
        >
          <!-- day -->
          <rect
            v-for="(d, i) in 7"
            :key="d"
            width="11"
            :title="d"
            height="11"
            x="16"
            :y="i * 15"
            rx="2"
            ry="2"
            fill="transparent"
          ></rect>

          <text
            x="16"
            :y="i * 15"
            v-for="(d, i) in 7"
            alignment-baseline="text-before-edge"
            :key="`w${d}`"
            rx="2"
            font-size="10"
            ry="2"
            fill="#adbac7"
          >
            {{ convertWeek(i) }}
          </text>
        </g>
      </g>
    </svg>
    <div class="example">
      <div>Less</div>
      <div>
        <span
          class="square"
          v-for="s in squares"
          :key="s.bgcolor"
          :style="`background:${s.bgcolor}`"
        ></span>
      </div>
      <div>More</div>
    </div>
  </div>
</template>

<script>
/*eslint-disable */
export default {
  name: "GithubWall",
  data() {
    return {
      groupDate: [],
      squares: [
        {
          bgcolor: "#282d34",
        },
        {
          bgcolor: "#103c25",
        },
        {
          bgcolor: "#01622c",
        },
        {
          bgcolor: "#229d39",
        },
        {
          bgcolor: "#32cd49",
        },
      ],
      testSum: [
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-05-04",
        "2022-04-04",
        "2022-02-04",
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-02-04",
        "2022-04-04",
        "2022-04-04",
        "2022-04-04",
        "2022-02-04",
        "2022-04-04",
        "2022-03-04",
        "2022-02-04",
        "2022-04-03",
        "2022-03-04",
        "2022-02-04",
        "2022-04-03",
        "2022-03-04",
        "2022-02-04",
        "2022-04-03",
        "2022-03-04",
        "2022-02-04",
        "2022-04-03",
        "2022-06-04",
        "2022-01-04",
        "2022-05-19",
        "2022-04-03",
        "2022-04-03",
        "2022-04-03",
        "2022-04-03",
        "2022-04-03",
        "2022-04-03",
        "2022-04-07",
        "2022-04-04",
        "2022-05-04",
        "2022-06-04",
        "2022-02-04",
        "2022-05-04",
        "2022-04-03",
        "2022-06-03",
        "2022-04-03",
        "2022-04-03",
        "2022-01-07",
        "2022-04-04",
        "2022-04-03",
        "2022-06-03",
        "2022-02-03",
        "2022-01-03",
        "2022-03-07",
        "2022-04-04",
        "2022-05-04",
        "2022-01-04",
        "2022-03-04",
        "2022-06-04",
        "2022-05-04",
        "2022-05-19",
        "2022-05-19",
        "2022-05-13",
        "2022-05-13",
        "2022-05-13",
        "2022-06-14",
        "2022-05-16",
        "2022-03-04",
        "2022-06-04",
        "2022-03-04",
        "2022-01-04",
        "2022-05-13",
        "2022-06-14",
        "2022-05-16",
        "2022-03-04",
        "2022-06-04",
        "2022-03-04",
        "2022-01-04",
        "2022-04-19",
        "2022-02-19",
        "2022-01-13",
        "2022-01-13",
        "2022-02-13",
        "2022-06-14",
        "2022-04-16",
        "2022-05-19",
      ],
    };
  },
  created() {
    this.dealDate("2022/01/01 - 2022/12/31");
    console.log(this.groupDate);
  },
  methods: {
    convertWeek(i) {
      let weekArr = ["Sun", "Mon", "Tue", "Wed", "Thu", "Fri", "Sat"];
      if ([1, 3, 5].indexOf(i) > -1) {
        return weekArr[i];
      }
      return "";
    },
    convertFill(d) {
      const s = this.computeContributies(d);
      if (s === 0) {
        return "#282d34";
      } else if (s <= 10) {
        return "#103c25";
      } else if (s <= 20) {
        return "#01622c";
      } else if (s <= 30) {
        return "#229d39";
      } else if (s > 30) {
        return "#32cd49";
      }
    },
    convertText(d) {
      const s = this.computeContributies(d);
      if (s === 1) {
        return `${s} contribution on ${d}`;
      }
      return `${s} contributions on ${d}`;
    },

    // 计算贡献次数
    computeContributies(d) {
      let s = this.testSum.filter((v) => {
        return d === v;
      });
      return s.length;
    },
    dealDate(splitDate) {
      // window.console.log(splitDate);
      //截取的开始时间
      var startTime = new Date(splitDate.split("-")[0].trim());
      console.log(startTime);
      //截取的结束时间
      var endTime = new Date(splitDate.split("-")[1].trim());
      console.log(endTime);
      //利用setTime获取两个日期之间差值,差值毫秒换算成天1000*60*60*24
      // window.console.log(startTime.getTime());
      let week = 0;
      var distanceDayLength =
        (endTime.getTime() - startTime.getTime()) / (1000 * 60 * 60 * 24);
      var startDay = startTime.getTime();
      for (let i = 0; i <= distanceDayLength; i++) {
        let key = i % 7;
        let temp = {};
        temp = this.$moment(
          new Date(startTime.setTime(startDay + 24 * 60 * 60 * 1000 * i))
        ).format("YYYY-MM-DD");
        if (this.groupDate[week]) {
          this.groupDate[week].push(temp);
        } else {
          this.groupDate[week] = [];
          this.groupDate[week].push(temp);
        }
        if (key == 0) {
          week += 1;
        }
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.github-wall {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: #1f2329;
  padding: 20px;
  .total {
    color: #adbac7;
    width: 880px;
    text-align: left;
    margin: 0 auto;
  }
  .day-rect {
    cursor: pointer;
    pointer-events: all;
  }
  .example {
    width: 880px;
    margin: 0 auto;
    color: #768390;
    display: flex;
    justify-content: flex-end;
    .square {
      display: inline-block;
      width: 10px;
      height: 10px;
      margin: 0 2px;
      border-radius: 2px;
    }
  }
}
</style>
