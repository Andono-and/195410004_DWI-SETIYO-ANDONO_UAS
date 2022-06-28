<template>
  <div>
    <div class="field">
      <label class="label">Product nama</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="Product nama"
          v-model="productnama"
        />
      </div>
    </div>
 
    <div class="field">
      <label class="label">harga</label>
      <div class="control">
        <input
          class="input"
          type="text"
          placeholder="harga"
          v-model="productharga"
        />
      </div>
    </div>
 
    <div class="control">
      <button class="button is-success" @click="saveProduct">SAVE</button>
    </div>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  nama: "AddProduct",
  data() {
    return {
      productnama: "",
      productharga: "",
    };
  },
  methods: {
    // Create New product
    async saveProduct() {
      try {
        await axios.post("http://localhost:5000/products", {
          product_nama: this.productnama,
          product_harga: this.productharga,
        });
        this.productnama = "";
        this.productharga = "";
        this.$router.push("/");
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
 
<style>
</style>