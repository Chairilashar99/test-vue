<template>
  <div class="center" id="app">
    <h2>{{ message }}</h2>
    <button @click="addNewItem" class="tambah">Tambah</button>
    <h4>Anda memiliki {{ listItem.length }} item.</h4>
    <div v-for="(item, index) in listItem" :key="item.id">
      {{ item.id }}
      <form @submit="handleSubmit($event, index)">
        <div class="formsec">
          <label>Product Name {{ index + 1 }}</label>
          <input
            type="text"
            v-model="item.name"
            placeholder="Enter product name"
          />
        </div>
        <div class="formsec">
          <label>Quantity</label>
          <input
            type="number"
            v-model="item.quantity"
            @input="handleChange(item)"
            placeholder="Enter product name"
          />
        </div>
        <div class="formsec">
          <label>Price </label>
          <input
            type="number"
            v-model="item.price"
            @input="item.total = item.price * item.quantity"
            placeholder="Enter product name"
          />
        </div>
        <div class="formsec">
          <label>Total Price </label>
          <input
            type="number"
            v-model="item.total"
            placeholder="Enter product name"
          />
        </div>
        <div class="formsec">
          <button>Delete</button>
        </div>
      </form>
    </div>
    <div class="formsec">
      <label>Total Purchase / Grand Total</label>
      <input class="right" type="number" :value="totalPrice" disabled />
    </div>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      listItem: [],
      message: "Welcome to Vue Shopping Chart-App",
    };
  },
  methods: {
    addNewItem() {
      this.listItem.push({
        id: 0,
        name: "",
        quantity: 1,
        price: 0,
        total: 0,
      });
    },
    handleSubmit: function (e, index) {
      e.preventDefault();
      let item = this.listItem[index];
      this.listItem = this.listItem.filter((it) => it != item);
    },
    handleChange: function (item) {
      if (item.quantity < 0) {
        alert("Jumlah Quantity tidak boleh kurang dari 0");
        item.quantity = 0;
      } else {
        item.total = item.price * item.quantity;
      }
    },
  },
  computed: {
    totalPrice: function () {
      let total = this.listItem.reduce((a, b) => a + b.total, 0);
      return this.listItem.length ? total : 0;
    },
  },
};
</script>

<style>
body {
  padding: 2em 10%;
  box-sizing: border-box;
  font-family: "Source Sans Pro", sans-serif;
}
.tambah {
  background: cornflowerblue;
  color: white;
  padding: 0.7em 1em;
  border: 1px solid cornflowerblue;
  border-radius: 0.4em;
  transition: all 0.3s;
}
.tambah:hover {
  cursor: pointer;
  background: rgb(65, 96, 153);
}
.formsec {
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
}

label {
  margin-bottom: 0.3em;
}
input {
  padding: 0.7em;
  border: 1px solid rgb(230, 230, 230);
  border-radius: 0.4em;
}
form {
  display: flex;
  gap: 1em;
  margin: 1em 0;
}
.formsec > button {
  display: inline-block;
  background: crimson;
  color: white;
  border: none;
  padding: 0.7em 1em;
  border-radius: 0.3em;
}
h4 {
  color: crimson;
}
.right {
  text-align: right;
  font-size: 1.2em;
  font-weight: 600;
}
</style>
