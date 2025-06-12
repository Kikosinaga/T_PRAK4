<template>
  <div class="product-page">
    <header class="page-header">
      <h1>Selamat Datang di Toko Fantasi Baby Pink!</h1>
      <p>Temukan produk impian Anda dengan sentuhan manis.</p>
    </header>

    <main class="product-list">
      <h2>Koleksi Kami</h2>
      <div class="product-grid">
        <ProductCard
          v-for="product in products"
          :key="product.id"
          :product="product"
          @add-to-cart="handleAddToCart"
        >
          <template v-slot:short-desc>
            <p v-if="product.id === 'p1'">Kamera canggih, abadikan momen indah dalam warna pink!</p>
            <p v-else-if="product.id === 'p2'">Laptop stylish dengan performa handal, cocok untuk gaya Anda.</p>
            <p v-else-if="product.id === 'p3'">Headphone nyaman dengan suara superior, temani hari-hari Anda.</p>
          </template>

          <template v-slot:badge>
            <span v-if="product.id === 'p1'" class="badge hot-pink">Pilihan Favorit!</span>
            <span v-else-if="product.id === 'p2'" class="badge soft-pink">Edisi Baru!</span>
            <span v-else-if="product.id === 'p3'" class="badge faded-pink">Diskon Spesial!</span>
          </template>

          <div>
            <p>Klik untuk melihat lebih banyak foto dan fitur.</p>
            <a href="#" @click.prevent="viewProductDetail(product.id)">Lihat Detail Produk</a>
          </div>
        </ProductCard>
      </div>
    </main>

    <aside class="shopping-cart">
      <h2>Keranjang Anda</h2>
      <div v-if="cartItems.length === 0" class="empty-cart">
        <p>Keranjang Anda masih kosong, ayo pilih produk favoritmu!</p>
      </div>
      <ul v-else class="cart-list">
        <li v-for="item in cartItems" :key="item.id + '-' + Math.random().toString(36).substring(7)">
          {{ item.name }} - Rp{{ item.price.toLocaleString('id-ID') }}
        </li>
      </ul>
      <p v-if="cartItems.length > 0" class="cart-total">
        Total: Rp{{ totalCartPrice.toLocaleString('id-ID') }}
      </p>
    </aside>

    <footer class="page-footer">
      <p>&copy; 2024 Toko Baby Pink. Dibuat dengan Cinta.</p>
    </footer>
  </div>
</template>

<script>
import { ref, computed } from 'vue';
import ProductCard from './components/ProductCard.vue'; // Pastikan path ini benar!

export default {
  components: {
    ProductCard
  },
  setup() {
    const products = ref([
      { id: 'p1', name: 'Sony Cybershot WX series Pink', price: 2499000, image: 'https://officepro.id/image/cache/data/journal2/Catalogue/Image/Products/Technology/Sony/DSC-WX220_PC-800x800.jpg' }, 
      { id: 'p2', name: 'MSI Prestige 14 Rose Pink Edition Laptop', price: 15699000, image: 'https://www.murdockcruz.com/wp-content/uploads/2020/02/Prestige-14-Limited-Edition-Rose-Pink.2.jpg' },
      { id: 'p3', name: 'Razer Kraken Bluetooth Headset Kitty - Quartz', price: 1599000, image: 'https://cdnpro.eraspace.com/media/catalog/product/r/a/razer_kraken_kitty_quartz_2_1.jpg' } 
    ]);

    const cartItems = ref([]);

    const handleAddToCart = (product) => {
      cartItems.value.push(product);
      console.log(`Produk "${product.name}" berhasil ditambahkan ke keranjang.`);
    };

    const totalCartPrice = computed(() => {
      return cartItems.value.reduce((sum, item) => sum + item.price, 0);
    });

    const viewProductDetail = (productId) => {
      alert(`Anda akan melihat detail produk dengan ID: ${productId}`);
    };

    return {
      products,
      cartItems,
      handleAddToCart,
      totalCartPrice,
      viewProductDetail
    };
  }
};
</script>

<style scoped>
.product-page {
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif; 
  max-width: 1200px;
  margin: 0 auto;
  padding: 30px; 
  background-color: #fff0f5; 
  border-radius: 15px; 
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  color: #333; 
}

.page-header {
  text-align: center;
  margin-bottom: 40px;
  background-color: #ffc0cb; 
  color: white; 
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.page-header h1 {
  margin-bottom: 10px;
  font-size: 2.8em; 
  text-shadow: 1px 1px 2px rgba(0, 0, 0, 0.1);
}

.page-header p {
  font-size: 1.2em;
}

.product-list {
  margin-bottom: 50px;
}

.product-list h2 {
  text-align: center;
  color: #e91e63; 
  margin-bottom: 30px;
  font-size: 2.5em;
  text-transform: uppercase; 
  letter-spacing: 2px;
}

.product-grid {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 25px; 
}

.shopping-cart {
  background-color: #ffe6f0; 
  padding: 30px;
  border-radius: 10px;
  border: 1px solid #ffd1dc; 
  margin-bottom: 50px;
  box-shadow: inset 0 2px 5px rgba(0, 0, 0, 0.05); 
}

.shopping-cart h2 {
  color: #e91e63;
  margin-bottom: 20px;
  text-align: center;
  font-size: 2em;
}

.empty-cart {
  text-align: center;
  color: #777;
  font-style: italic;
  padding: 15px;
  background-color: #fce8f0;
  border-radius: 5px;
}

.cart-list {
  list-style-type: none;
  padding: 0;
  margin-bottom: 20px;
}

.cart-list li {
  background-color: #fffafa;
  border: 1px solid #ffe8ed;
  padding: 12px;
  margin-bottom: 8px;
  border-radius: 6px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 1.05em;
  color: #444;
}

.cart-total {
  font-weight: bold;
  font-size: 1.4em;
  text-align: right;
  color: #e91e63; 
  border-top: 2px dashed #ffc0cb; 
  padding-top: 15px;
  margin-top: 15px;
}

.page-footer {
  text-align: center;
  color: #a05252; 
  font-size: 1em;
  padding-top: 25px;
  border-top: 1px solid #ffd1dc;
  margin-top: 30px;
}

.badge {
  display: inline-block;
  padding: 6px 12px;
  border-radius: 20px;
  font-size: 0.85em;
  font-weight: bold;
  color: white;
  margin-left: 8px;
  text-transform: uppercase;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}

.badge.hot-pink {
  background-color: #e91e63; 
}

.badge.soft-pink {
  background-color: #ff69b4; 
}

.badge.faded-pink {
  background-color: #ff99cc; 
}

a {
  color: #da70d6; 
  text-decoration: none;
  font-weight: 500;
}

a:hover {
  text-decoration: underline;
  color: #c71585; 
}
</style>