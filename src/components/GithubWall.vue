<template>
  <div class="github-wall">
    <svg width="100%" height="200">
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
            :title="d"
            height="11"
            x="16"
            :y="i * 15"
            rx="2"
            ry="2"
            :fill="`rgb(${Math.round(Math.random() * 255)},${Math.round(
              Math.random() * 255
            )},${Math.round(Math.random() * 255)})`"
          ></rect>
        </g>
        <!-- week -->
        <g
          :transform="`translate(-16, 0)`"
          v-for="(item, index) in 1"
          :key="index"
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
          ></rect>

          <text
            x="16"
            :y="i * 15"
            v-for="(d, i) in 7"
            style="width: 11px; height: 11px"
            :key="d"
            rx="2"
            font-size="11"
            ry="2"
            fill="red"
          >
            s
          </text>
        </g>
      </g>
    </svg>
  </div>
</template>

<script>
/*eslint-disable */
export default {
  name: "GithubWall",
  data() {
    return {
      groupDate: [],
    };
  },
  created() {
    this.dealDate("2021/01/01 - 2022/12/31");
    console.log(this.groupDate);
  },
  methods: {
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
<style scoped lang="less"></style>
