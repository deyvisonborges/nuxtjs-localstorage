<template>
    <div>
        <div v-for="(product, index) in product_list" :key="index">
            <p>{{ product }}</p>
        </div>
        <form action="" @submit.prevent="addProductToCart">
            code: <input type="text" v-model="form_code" autofocus> <br>
            name: <input type="text" v-model="form_name"> <br>
            price: <input type="text" v-model="form_price"> <br>
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

    methods: {
        addProductToCart() {
            this.product_list.push(
                {
                    code: this.form_code,
                    name: this.form_name,
                    price: this.form_price
                }
            );
            this.saveProducts();
            return;
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