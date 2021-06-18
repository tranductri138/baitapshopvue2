<template>
  <div>
    <Header />
  </div>
  <div class="choose">
    <div class="choosebl">
      <select name="chose" @change="sortBy">
        <option value="sort-asc">Price low to hight</option>
        <option value="sort-desc">Price hight to low</option>
        <option value="sorta-z">Name a to z</option>
        <option value="sortz-a">Name z to a</option>
      </select>
    </div>
    <p>Select value is : {{ msg }}</p>
    <div class="choosebl">
      <select name="chose" id="chooose2">
        <option value="volvo">1000 - 200000</option>
        <option value="saab">Saab</option>
        <option value="mercedes">Mercedes</option>
        <option value="audi">Audi</option>
      </select>
    </div>
  </div>
  <div class="container">
    <div class="block" v-for="item in motorbikes" :key="item.id">
      <img :src="item.image" alt="" />
      <h3>{{ item.name }}</h3>
      <p>{{ item.price }} VND</p>
    </div>
    <div>
      <h3>Tổng số sản phẩm : {{ motorbikes.length }}</h3>
      <h3>Tổng số tiền tất cả các sản phẩm : {{ totalPriceOfMotor() }} VND</h3>
      <h3>Tổng số tiền tất cả các sản phẩm : {{ avgPriceOfMotor() }} VND</h3>
    </div>
  </div>
</template>

<script>
import Header from "./components/Header.vue";

export default {
  name: "App",
  components: { Header },
  data() {
    return {
      motorbikes: [
        {
          id: 0,
          name: "Wave alpha",
          price: 19000000,
          image: require("@/assets/xe_wavea.jpg"),
        },
        {
          id: 1,
          name: "Dream",
          price: 18000000,
          image: require("@/assets/xe_dream.jpg"),
        },
        {
          id: 2,
          name: "Sirius",
          price: 21000000,
          image: require("@/assets/xe_sirius.jpg"),
        },
        {
          id: 3,
          name: "Air Blade",
          price: 35000000,
          image: require("@/assets/xe_airblade.jpg"),
        },
        {
          id: 4,
          name: "Raider",
          price: 45000000,
          image: require("@/assets/xe_raider.jpg"),
        },
        {
          id: 5,
          name: "Sh",
          price: 90000000,
          image: require("@/assets/xe_sh.jpg"),
        },
      ],
      msg: "...",
    };
  },
  methods: {
    countProduct() {
      const product = this.motorbikes.filter((motorbike) => motorbike.id);
      return product.length;
    },
    totalPriceOfMotor() {
      let sum = 0;
      this.motorbikes.forEach((motorbike) => {
        sum += motorbike.price;
      });
      return sum;
    },
    avgPriceOfMotor() {
      return (this.totalPriceOfMotor() / this.motorbikes.length).toFixed(2);
    },
    sortBy(event) {
      console.log(event.target.value);
      this.msg = event.target.value;
      if (event.target.value == "sort-asc") {
        this.motorbikes = this.sortByPrice(this.motorbikes, "asc");
      } else if (event.target.value == "sort-desc") {
        this.motorbikes = this.sortByPrice(this.motorbikes, "desc");
      } else if (event.target.value == "sorta-z") {
        this.motorbikes = this.sortByName(this.motorbikes, "asc");
      } else if (event.target.value == "sortz-a") {
        this.motorbikes = this.sortByName(this.motorbikes, "desc");
      }
    },
    sortByPrice(motor, compare) {
      if (compare == "asc") {
        motor.sort(function (a, b) {
          return a.price - b.price;
        });
        return motor;
      } else if (compare == "desc") {
        motor.sort(function (a, b) {
          return -a.price + b.price;
        });
        return motor;
      }
    },
    sortByName(motor, compare) {
      if (compare == "asc") {
        motor.sort(function (a, b) {
          return a.name.localeCompare(b.name);
        });
        return motor;
      } else if (compare == "desc") {
        motor.sort(function (a, b) {
          return b.name.localeCompare(a.name);
        });
        return motor;
      }
    },
  },
};
</script>

<style>
.container {
  margin: auto;
  width: 70%;
  display: flex;
  padding: 40px;
  flex-wrap: wrap;
}
img {
  width: 300px;
  height: 210px;
}
.block {
  margin: 10px;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.choose {
  display: flex;
  justify-content: center;
}
.choosebl {
  margin: 60px;
}
</style>
