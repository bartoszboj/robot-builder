<template>
  <div class="wrapper">
    <button class="add-to-cart" @click="addToCart()">Add to Cart</button>
    <div class="top-row">
        <!-- <div class="robot-name">
          {{ selectedRobot.head.title }}
          <span class="sale" v-if="selectedRobot.head.onSale">Sale!!!</span>
        </div> -->
        <part-selector 
        :parts="availableParts.heads"
        :position="top"/>
    </div>
    <div class="middle-row">
      <part-selector 
      :parts="availableParts.arms"
      position="left"/>

      <part-selector 
      :parts="availableParts.torsos"
      position="center"/>

      <part-selector 
      :parts="availableParts.arms"
      position="right"/>
    </div>
    <div class="bottom-row">
        <part-selector 
        :parts="availableParts.bases"
        position="bottom"/>
    </div>
    <div class="cart">
      <h1>Cart</h1>
      <table>
        <thead>
          <tr>
            <th>Robot</th>
            <th class="cost">Cost</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(robot, key) in cart" :key="key">
            <td>{{ robot.head.title }}</td>
            <td class="cost">{{ robot.totalCost }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import availableParts from "@/components/data/parts";
import createdHookMixin from "./created-hook-mixin.js";
import PartSelector from "@/components/builder/PartSelector.vue";

export default {
  name: "RobotBuilder",
  mixins: [createdHookMixin],
  components: {
    PartSelector
  },
  data() {
    return {
      cart: [],
      availableParts,
    };
  },
  computed: {
    selectedRobot() {
      return{
        head: availableParts.heads[this.headIndex],
        leftArm: availableParts.arms[this.leftArmIndex],
        torso: availableParts.torsos[this.torsoIndex],
        rightArm: availableParts.arms[this.rightArmIndex],
        base: availableParts.bases[this.baseIndex]
      }
    },
  },
  methods: {
    isOnSale(item) {
      return item.onSale
    },
    addToCart() {
      const robot = this.selectedRobot;
      let totalCost = 0;
      Object.keys(robot).forEach(item => {
        totalCost += robot[item].cost;
      })
      this.cart.push(Object.assign({}, robot, { totalCost }))
    },
  },
};
</script>

<style lang="scss" scoped>
  .wrapper{
    position: relative;
  }
  .top-row {
    display: flex;
    justify-content: space-around;
  }
  .middle-row {
    display: flex;
    justify-content: center;
  }
  .bottom-row {
    display: flex;
    justify-content: space-around;
    border-top: none;
  }
  .head {
    border-bottom: none;
  }
  .left {
    border-right: none;
  }
  .right {
    border-left: none;
  }
  .left img {
    transform: rotate(-90deg);
  }
  .right img {
    transform: rotate(90deg) scale(-1, 1);
  }
  .bottom {
    border-top: none;
  }
  .center .prev-selector,
  .center .next-selector {
    opacity: 0.8;
  }
  .left .prev-selector {
    top: -28px;
    left: -3px;
    width: 144px;
    height: 25px;
  }
  .left .next-selector {
    top: auto;
    bottom: -28px;
    left: -3px;
    width: 144px;
    height: 25px;
  }
  .right .prev-selector {
    top: -28px;
    left: 24px;
    width: 144px;
    height: 25px;
  }
  .right .next-selector {
    top: auto;
    bottom: -28px;
    left: 24px;
    width: 144px;
    height: 25px;
  }
  .right .next-selector {
    right: -3px;
  }
  .robot-name{
    position: absolute;
    width: 100%;
    top: -27px;
    text-align: center;

    .sale{
      color: white;
      background-color: red;
      border-radius: 15px;
      padding: 3px;
      margin-left: 5px;
    }
  }
  .add-to-cart{
    position: absolute;
    right: 30px;
    width: 200px;
    padding: 5px 10px;
    font-size: 16px;
  }
  td, th {
    padding: 5px;
    padding-right: 20px;
    text-align: left;
  }
  .cost{
    text-align: right;
  }
  .sale-border{
    border: 3px solid red;
  }
</style>
