<template>
  <div class="product-card">
    <img :src="product.image" :alt="product.name" class="product-image" />
    <h3 class="product-name">{{ product.name }}</h3>
    <p class="product-price">Harga: Rp{{ product.price.toLocaleString('id-ID') }}</p>

    <div class="product-description">
      <slot name="short-desc">
        <p>Deskripsi singkat default produk ini.</p>
      </slot>
    </div>

    <div class="product-badge">
      <slot name="badge"></slot>
    </div>

    <div class="additional-content">
      <slot></slot>
    </div>

    <AddToCartButton @item-added="handleAddToCart" class="mt-3">
      Beli Sekarang!
    </AddToCartButton>
  </div>
</template>

<script>
import AddToCartButton from './AddToCartButton.vue';

export default {
  components: {
    AddToCartButton
  },
  props: {
    product: {
      type: Object,
      required: true,
      default: () => ({
        id: 'default',
        name: 'Produk Default',
        price: 0,
        image: 'https://via.placeholder.com/150'
      })
    }
  },
  emits: ['add-to-cart'],
  setup(props, { emit }) {
    const handleAddToCart = () => {
      emit('add-to-cart', props.product);
      console.log(`Produk "${props.product.name}" siap ditambahkan ke keranjang.`);
    };

    return {
      handleAddToCart
    };
  }
};
</script>

<style scoped>
.product-card {
  border: 1px solid #ffdde1; 
  border-radius: 12px; 
  padding: 20px;
  margin: 15px;
  width: 280px;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.08); 
  text-align: center;
  background-color: #ffffff; 
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  transition: transform 0.2s ease, box-shadow 0.2s ease; 
}

.product-card:hover {
  transform: translateY(-5px); 
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.15); 
}

.product-image {
  width: 100%;
  max-height: 180px;
  object-fit: cover;
  border-radius: 8px; 
  margin-bottom: 15px;
  border: 1px solid #ffe8ed; 
}

.product-name {
  font-size: 1.5em; 
  color: #333;
  margin-bottom: 8px;
  font-weight: 600; 
}

.product-price {
  font-size: 1.3em;
  color: #e44d26; 
  font-weight: bold;
  margin-bottom: 15px;
}

.product-description, .additional-content {
  font-size: 0.95em; 
  color: #555;
  margin-bottom: 10px;
}

.product-badge {
  margin-top: 5px;
  margin-bottom: 10px;
}

.mt-3 {
  margin-top: auto; 
}
</style>