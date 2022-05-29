<script>
import { findProp } from "@vue/compiler-core";

export default {
  data() {
    return {
      dice: [
        {
          id: 1,
          value: 1,
        },
        {
          id: 2,
          value: 1,
        },
        {
          id: 3,
          value: 1,
        },
        {
          id: 4,
          value: 1,
        },
        {
          id: 5,
          value: 1,
        },
      ],
      loading: false,
      equals: [],
      unequals: [],
    };
  },
  methods: {
    roll: function () {
      this.equals = [];
      this.unequals = [];

      for (let i = 0; i < 5; i++) {
        this.dice[i].value = 1 + Math.floor(Math.random() * 6);
      }
      this.split(this.dice);
    },
    split: function (arr) {
      var counts = [
        {
          number: 1,
          count: 0,
        },
        {
          number: 2,
          count: 0,
        },
        {
          number: 3,
          count: 0,
        },
        {
          number: 4,
          count: 0,
        },
        {
          number: 5,
          count: 0,
        },
        {
          number: 6,
          count: 0,
        },
      ];

      for (let i = 0; i < arr.length; i++) {
        counts[arr[i].value - 1].count++;
      }

      for (let i = 0; i < counts.length; i++) {
        if (counts[i].count == 0) {
        } else if (counts[i].count == 1) {
          this.unequals.push(counts[i].number);
        } else {
          var eq_group = [];

          for (let j = 0; j < counts[i].count; j++) {
            eq_group.push(counts[i].number);
          }

          this.equals.push(eq_group);
        }
      }
    },
  },
};
</script>

<template>
  <main>
    <section class="diceWrapper">
      <TransitionGroup class="diceGroup colorful" name="foo" tag="ul">
        <li
          v-for="item in this.unequals"
          :key="Math.random() * item"
          class="dieFace"
        >
          <span>{{ item }}</span>
        </li>
      </TransitionGroup>

      <TransitionGroup class="diceGroup green" name="foo" tag="ul">
        <li
          v-for="item in this.equals[0]"
          :key="Math.random() * item"
          class="dieFace"
        >
          <span>{{ item }}</span>
        </li>
      </TransitionGroup>

      <TransitionGroup class="diceGroup blue" name="foo" tag="ul">
        <li
          v-for="item in this.equals[1]"
          :key="Math.random() * item"
          class="dieFace"
        >
          <span>{{ item }}</span>
        </li>
      </TransitionGroup>
    </section>
    <button class="rollButton" :disabled="this.loading" @click="this.roll()">
      ROLL & SPLIT
      <span
        >Rolls 5 dice, and splits them into groups of equals and unequals</span
      >
    </button>
  </main>
</template>

<style lang="css">
body {
  background: #f2e9e4;
}
.foo-enter-active {
  transition: all 0.6s cubic-bezier(0.33, 1, 0.68, 1);
}
.foo-leave-active {
}
.foo-enter-from {
  transform: rotate(-360deg);
  opacity: 0;
}
.foo-leave-to {
}

main {
  margin: auto;
  width: 100%;
  display: flex;
  flex-flow: column;
  height: 100vh;
  justify-content: space-between;
}
.rollButton {
  width: 90%;
  margin: 0 auto 50px auto;
  max-width: 375px;
  height: 100px;
  border: none;
  border-radius: 16px;
  background: #223f5a;
  color: white;
  font-size: 18px;
  font-weight: 800;
  display: flex;
  flex-flow: column;
  justify-content: center;
  align-items: center;
  box-shadow: 0 10px #08203e, 10px 10px 10px rgb(169, 168, 154);
  transition: all 0.15s ease-out;
}

.rollButton span {
  font-size: 12px;
  opacity: 0.7;
  margin-top: 10px;
  max-width: 60%;
}
.rollButton:hover {
  cursor: pointer;
  box-shadow: 0 5px #08203e, 5px 5px 5px rgb(169, 168, 154);
  transform: translateY(5px);
}
.rollButton:active {
  box-shadow: none;
  transform: translateY(10px);
}

.diceWrapper {
  margin-top: 50px;
  display: flex;
  flex-flow: column;
  justify-content: center;
}
.diceGroup {
  display: flex;
  flex-flow: row;
  flex-wrap: wrap;
  margin-bottom: 15px;
  padding-bottom: 5px;
  border-bottom: 4px solid #eed9d4;
  box-shadow: 0 2px #ffffff;
  min-height: 110px;
  justify-content: center;
  padding-left: 0;
}

.dieFace {
  width: 80px;
  height: 80px;
  border-radius: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-right: 10px;
  color: white;
  margin-bottom: 15px;
  position: relative;
}
.diceGroup.green .dieFace {
  background: #3bacb6;
  color: white;
  box-shadow: 0 5px #318c94, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.blue .dieFace {
  background: #9eb708;
  border: none;
  color: white;
  box-shadow: 0 5px #839809, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.colorful .dieFace:first-child {
  background: #fc6462;
  box-shadow: 0 5px #e15a57, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.colorful .dieFace:nth-child(2) {
  background: #faa03c;
  box-shadow: 0 5px #d58a33, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.colorful .dieFace:nth-child(3) {
  background: #fb8c49;
  box-shadow: 0 5px #c66f39, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.colorful .dieFace:nth-child(4) {
  background: #fab430;
  box-shadow: 0 5px #db9d29, 5px 5px 5px rgb(169, 168, 154);
}
.diceGroup.colorful .dieFace:nth-child(5) {
  background: #fb7855;
  box-shadow: 0 5px #d36648, 5px 5px 5px rgb(169, 168, 154);
}

.dieFace:first-child {
  transition-delay: 0;
}
.dieFace:nth-child(2) {
  transition-delay: 0.1s;
}
.dieFace:nth-child(3) {
  transition-delay: 0.2s;
}
.dieFace:nth-child(4) {
  transition-delay: 0.3s;
}
.dieFace:nth-child(5) {
  transition-delay: 0.4s;
}
.dieFace span {
  font-size: 30px;
  font-weight: 800;
}
</style>
