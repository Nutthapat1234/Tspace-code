<template>
  <div>
    <div style="text-align: center">
      <p style="margin: 0px">Rules</p>
      <p
        style="
          display: inline-block;
          margin: 0px;
          font-size: 20px;
          text-align: left;
        "
      >
        1.red win against green<br />
        2. green win against brown<br />
        3. brown win against blue <br />
        4. blue win against red
      </p>
    </div>
    <button v-on:click="select($event)" style="background: red"></button>
    <button v-on:click="select($event)" style="background: blue"></button>
    <button v-on:click="select($event)" style="background: green"></button>
    <button v-on:click="select($event)" style="background: brown"></button>
  </div>
  <div>
    <p>
      {{ pre_result }}    <b style="font-size: 30px;">{{ result }}</b>
    </p>
    <button id="comparebutton" v-on:click="compare()">Compare</button>
  </div>
</template>

<script>
export default {
  name: "Box",
  data() {
    return {
      rules: ["blue", "brown", "green", "red"], // game rules: blue-> brown-> green-> red-> blue
      default_color: ["red", "blue", "green", "brown"], // default buttons color
      select_color: null, // user select
      pre_result: "",
      result: "",
    };
  },
  methods: {
    select(e) {
      // label selected color
      for (let i = 0; i < this.default_color.length; i++) {
        document.getElementsByTagName("button")[i].style.border =
          this.default_color[i];
      }
      if (e.currentTarget.style.border.localeCompare(this.select_color) == 0){
          this.select_color = null;
      }
      else{
          e.currentTarget.style.border = "5px solid black";
          this.select_color = e.currentTarget.style.background;
      }
    },

    compare() {
      // compare color
      if (this.select_color === null) {
        this.pre_result = "";
        this.result = "Select color First";
        return;
      }
      let index = this.rules.indexOf(this.select_color);
      // random color using number as color 0: blue, 1: brown, 2:green, 3:red
      let rand_color = Math.floor(Math.random() * 4);
      let win_index = index + 1;
      let lose_index = index - 1;

      if (win_index == 4) win_index = 0;
      else if (lose_index < 0) lose_index = 3;
      // game condition
      if (rand_color == win_index) {
        this.pre_result =
          `Player select ${this.rules[index]};  ` +
          `System select ${this.rules[rand_color]};  `;
        this.result = `System win`;
      } else if (rand_color == lose_index) {
        this.pre_result =
          `Player select ${this.rules[index]};  ` +
          `System select ${this.rules[rand_color]};  `;
        this.result = `Player win`;
      } else {
        this.pre_result = 
          `Player select ${this.rules[index]};  ` +
          `System select ${this.rules[rand_color]};  `;
        this.result = "Draw";
      }
    },
  },
};
</script>

<style scoped>
button {
  width: 250px;
  height: 200px;
  margin: 20px;
}
p {
  margin-top: 20px;
  font-size: 25px;
}
#comparebutton {
  width: 90%;
  height: 100px;
}
</style>