<template>
  <button @click="addToCart" class="add-to-cart-btn">
    <slot>Tambah ke Keranjang</slot>
  </button>
</template>

<script>
export default {
  emits: ['item-added'],
  setup(props, { emit }) {
    const addToCart = () => {
      emit('item-added');
      console.log('Tombol Tambah ke Keranjang diklik!');
    };

    return {
      addToCart
    };
  }
};
</script>

<style scoped>
.add-to-cart-btn {
  /* Warna tombol menjadi pink yang lebih gelap */
  background-color: #ffb6c1; /* LightPink */
  color: #333; /* Teks lebih gelap agar terbaca */
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 1em;
  transition: background-color 0.2s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1); /* Tambah sedikit bayangan */
}

.add-to-cart-btn:hover {
  background-color: #ff9ca9;
  transform: translateY(-1px); 
}
</style>