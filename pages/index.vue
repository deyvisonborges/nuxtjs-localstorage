<template>
    <div>
        <div :for="(product, index) in product_list">
            <ul>
                <li>{{product}}</li>
            </ul>
            <button @click="removeProductByCode(index)"></button>
        </div>
        <form action="" @submit.prevent="addProductToCart">
            code: <input type="text" v-model="code"> <br>
            name: <input type="text" v-model="name"> <br>
            price: <input type="text" v-model="price"> <br>
            <button type="submit"> persist </button>
        </form>
    </div>
</template>

<script>
export default {
    data() {
        return {
            product_list: []
        }
    },
    watch: {
        product_list(product_list) {
            this.product_list = product_list;
        }
    },

    methods: {
        addProductToCart() {
            this.product_list.push({
                code: this.code,
                name: this.name,
                price: this.price
            })
    
            this.saveProducts();
        },

        removeProductByCode(index) {
            this.product_list.splice(index, 1);
            this.saveProducts();
        },

        saveProducts() {
            let parsed = JSON.stringify(this.product_list);
            localStorage.setItem('product_cart', parsed);
        }
    }
}
</script>

<style>

</style>