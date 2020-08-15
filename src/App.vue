<template>
  <div id="app">
    <h1>Welcome to Uniqlo</h1>
    <div class="ItemCard">
      <div class="ItemCard--image">
        <img v-bind:src="items[currentItem].imgSrc" />
      </div>
      <div class="ItemCard--selection">
        <h2>Uniqlo Oversized T-Shirt</h2>
        <div class="ItemCard--selection--colours">
          <p>Colours:</p>
          <ul>
            <li v-for="(item, index) in items" :key="index">
              <input
                  type="radio"
                  :id="'tshirt-' + item.variant"
                  name="tshirt"
                  v-on:click="updateSelection(index)"
                  :style="{
                    backgroundColor: item.hex
                  }"
              />
            </li>
          </ul>
        </div>
        <div class="ItemCard--selection--sizes">
          <p>Sizes:</p>
          <ul>
            <li>
              <input
                  type="radio"
                  :id="'tshirt-size-s-' + items[currentItem].variant"
                  name="tshirt-size"
                  :disabled="items[currentItem].availability.s <= 0"
                  @click="updateSelectedSize(`s`)"
              />
              <label :for="'tshirt-size-s-' + items[currentItem].variant">Small</label>
            </li>
            <li>
              <input
                  type="radio"
                  :id="'tshirt-size-m-' + items[currentItem].variant"
                  name="tshirt-size"
                  :disabled="items[currentItem].availability.m <= 0"
                  @click="updateSelectedSize(`m`)"
              />
              <label :for="'tshirt-size-m-' + items[currentItem].variant">Medium</label>
            </li>
            <li>
              <input
                  type="radio"
                  :id="'tshirt-size-l-' + items[currentItem].variant"
                  name="tshirt-size"
                  :disabled="items[currentItem].availability.l <= 0"
                  @click="updateSelectedSize(`l`)"
              />
              <label :for="'tshirt-size-l-' + items[currentItem].variant">Large</label>
            </li>
          </ul>
        </div>
        <div class="ItemCard--selection--quantity">
          <label>Quantity:</label>
          <input
              type="number"
              min="0"
              :max="items[currentItem].availability[selectedSize]"
              :value="items[currentItem].availability[selectedSize] > 0 ? 1 : 0"
          />
        </div>
      </div>
    </div>
  </div>
</template>



<script>
  export default {
    name: 'App',
    components: {

    },
    methods: {
      updateSelection(index) {
        this.currentItem = index;
      },
      updateSelectedSize(size) {
        this.selectedSize = size;
      }
    },
    data() {
      return {
        currentItem: 0,
        selectedSize: `s`,
        items: [
          {
            variant: `white`,
            hex: `#ffffff`,
            availability: {
              s: 4,
              m: 0,
              l: 1
            },
            imgSrc: require(`./assets/images/tshirt-white.jpg`)
          },
          {
            variant: `black`,
            hex: `#000000`,
            availability: {
              s: 2,
              m: 2,
              l: 2
            },
            imgSrc: require(`./assets/images/tshirt-black.jpg`)
          },
          {
            variant: `brown`,
            hex: `#78533e`,
            availability: {
              s: 9,
              m: 4,
              l: 3
            },
            imgSrc: require(`./assets/images/tshirt-brown.jpg`)
          },
          {
            variant: `navy`,
            hex: `#3e3b50`,
            availability: {
              s: 5,
              m: 7,
              l: 9
            },
            imgSrc: require(`./assets/images/tshirt-navy.jpg`)
          }
        ]
      }
    }
  }
</script>



<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  text-align: center;
}

.ItemCard {
  display: flex;
  justify-content: space-around;
  width: 960px;
  padding: 4rem 3.6rem;
  box-shadow: 0 0 22px 0 #ccc;
  margin: 120px auto;
  border-radius: 15px;
  transition: box-shadow 250ms ease-in-out;
}

.ItemCard:hover {
  box-shadow: 0 0 10px 0 #dfdfdf;
}

.ItemCard--image {
  width: 40%;
}

.ItemCard--image img {
  width: 100%;
}

.ItemCard--selection {
  width: 50%;
}

.ItemCard--selection--colours,
.ItemCard--selection--sizes,
.ItemCard--selection--quantity {
  padding-top: 32px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

.ItemCard--selection--colours p,
.ItemCard--selection--sizes p,
.ItemCard--selection--quantity label {
  font-weight: 500;
  width: 20%;
}

.ItemCard--selection--colours ul,
.ItemCard--selection--sizes ul {
  list-style-type: none;
}

.ItemCard--selection--sizes ul li,
.ItemCard--selection--quantity input {
  display: inline-block;
  margin-left: 14px;
}

.ItemCard--selection--quantity input {
  width: 80px;
  padding: 0.5rem;
  border-radius: 0;
  border: 1px solid #000;
  -moz-outline-radius: 0;
}

.ItemCard--selection--sizes ul li label {
  padding: 0.3rem 0.8rem;
  border: 1px solid #000;
  cursor: pointer;
}

.ItemCard--selection--sizes ul li input:checked + label {
  background-color: #000;
  color: #fff;
}

.ItemCard--selection--sizes ul li input:disabled + label {
  opacity: 0.3;
  cursor: default;
}

.ItemCard--selection--sizes ul li input {
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  cursor: pointer;
}

.ItemCard--selection--colours ul li {
  width: 32px;
  height: 32px;
  margin-left: 14px;
  display: inline-block;
  padding: 4px;
  border: 1px solid #000;
}

.ItemCard--selection--colours ul li input {
  width: 100%;
  height: 100%;
  -webkit-appearance: none;
  -moz-appearance: none;
  appearance: none;
  cursor: pointer;
}

.ItemCard--selection--colours ul li input:checked {
  box-shadow: 0 0 0 6px #000;
}
</style>
