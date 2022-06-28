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
      <button class="button is-success" @click="updateProduct">UPDATE</button>
    </div>
  </div>
</template>
 
<script>
// import axios
import axios from "axios";
 
export default {
  nama: "EditProduct",
  data() {
    return {
      productnama: "",
      productharga: "",
    };
  },
  created: function () {
    this.getProductById();
  },
  methods: {
    // Get Product By Id
    async getProductById() {
      try {
        const response = await axios.get(
          `http://localhost:5000/products/${this.$route.params.id}`
        );
        this.productnama = response.data.product_nama;
        this.productharga = response.data.product_harga;
      } catch (err) {
        console.log(err);
      }
    },
 
    // Update product
    async updateProduct() {
      try {
        await axios.put(
          `http://localhost:5000/products/${this.$route.params.id}`,
          {
            product_nama: this.productnama,
            product_harga: this.productharga,
          }
        );
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