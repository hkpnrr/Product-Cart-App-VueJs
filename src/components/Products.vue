<template>
<div v-if="productList.length>0">
    <h3 class="text-center">List of Added Products</h3>
    <hr>
    <div class="row product-container">
        <appProduct v-for="product in productList">
            <img class="card-img-top" :src="product.selectedImage == null ? '/src/assets/default.png' : product.selectedImage" alt="Card image cap">
            <div class="card-body">
                <h5 class="card-title">{{product.title }}</h5>
                <small><strong>Amount : </strong> {{ product.count }}</small>
                <br>
                <small><strong>Price : </strong> {{ product.price }}</small>
                <br>
                <small><strong>Total Price : </strong> {{product.totalPrice}}</small>
            </div>
        </appProduct>
    </div>
</div>
</template>

<script>
import Product from './Product.vue'
import {
    eventBus
} from '../main'

export default {

    components: {
        appProduct: Product
    },
    data() {
        return {
            productList: [],

        }
    },
    created() {
        eventBus.$on('addedProduct', (product) => {
            if (this.productList.length < 5) {
                this.productList.push(product);
                eventBus.$emit('updateProgressBar', this.productList.length);
            } else {
                alert("ürün sayısı 5'den fazla olamaz!")
            }
        })
    }
}
</script>
