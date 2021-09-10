<script>
export default {
  data() {
    return {
      input: "",
      question: "",
      answer: [],
      times: 0,
      tableData: [{ times: "我是例子", guess: "1234", result: "0A0B" }],
    };
  },
  mounted() {
    const num = ["0", "1", "2", "3", "4", "5", "6", "7", "8", "9"];
    var ques = [];
    for (var i = 0; i < 4; i++) {
      var idx = Math.floor(Math.random() * num.length);
      ques.push(num[idx]);
      num.splice(idx, 1);
    }
    this.question = ques;
    // console.log(this.question);
  },
  methods: {
    addAns() {
      this.check();
      if (this.input != "" && this.input.length == 4) {
        this.times += 1;
        this.tableData.push({
          times: this.times,
          guess: this.input,
          result: this.answer,
        });
        this.input = "";
      } else {
        alert("請輸入4位數數字");
      }
    },
    check() {
      var a = 0;
      var b = 0;
      var input = this.input;

      for (var i = 0; i < 4; i++) {
        var idx = this.question.indexOf(input[i]);
        if (idx != -1) {
          if (idx == i) {
            a++;
          } else {
            b++;
          }
        }
      }
      if (a == 4) {
        alert("答對了!");
      }
      this.answer = a + "a" + b + "b";
    },
    clear() {
      this.tableData = [];
      this.times = 0;
    },
  },
};
</script>

<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
    <h1>1A2B(不含重複數字)</h1>
    <!-- 反白可以看答案 -->
    <h3>{{ question }}</h3>
    <!-- 反白可以看答案 -->

    <el-main>
      <el-card class="box-card">
        <template #header>
          <el-button @click="clear" type="danger" style="width: 100%"
            >清空歷史紀錄</el-button
          >
          <el-input
            v-model="input"
            placeholder="輸入4位數數字後送出或enter"
            @keyup.enter="addAns()"
          ></el-input>
          <el-button @click="addAns" type="primary" style="width: 100%"
            >送出</el-button
          >
        </template>
        <el-table
          :data="tableData"
          style="width: 100%"
          :header-cell-style="{
            'background-color': '#2c3e50',
            color: '#fff',
            'font-weight': '400',
          }"
        >
          <el-table-column prop="times" label="第幾次猜" align="center">
          </el-table-column>
          <el-table-column prop="guess" label="這次猜" align="center">
          </el-table-column>
          <el-table-column prop="result" label="結果" align="center">
          </el-table-column>
        </el-table>
      </el-card>
    </el-main>
  </div>
</template>

<style>
body {
  background-color: #e9eef3;
}
h3 {
  color: #e9eef3;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.el-main {
  display: flex;
  justify-content: center;
  align-items: center;
}

.el-input__inner {
  text-align: center;
}
</style>
