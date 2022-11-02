<template>
    <div class="container">
        <div class="mt-5 ">
            <h2 class="text-center font-weight-normal " style="font-family: Arial, Helvetica, sans-serif;">List Product</h2>
            <div class="mt-5 card-body ">
                <div class="d-flex justify-content-center row">
                    <div class="col-sm-3 card ml-4 mb-4 " v-for="(product) in products" :key="product.id">
                        <center>
                            <img :src="`http://localhost:8000/storage/${product.image}`" height="200" class=""/>
                        </center>
                        <div class="card-body mt-2 p-4">
                            <div class="card-body" align="right">
                                <h5 class="card-title">{{ product.title }}</h5>
                                <p class="card-text">Harga Rp.{{ product.price }}</p>

                                <router-link class="btn btn-primary btn-sm rounded shadow"
                                    :to="{   name: 'editpage', params: {id: product.id} }">edit</router-link>&nbsp;

                                <button class="btn btn-danger btn-sm rounded shadow"
                                    @click.prevent="delProduct(product.id)">Delete</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios";

export default {
    data() {
        return {
            products: Array,
        };
    },
    created() {
        this.getProduct();
    },
    methods: {
        async getProduct() {
            let url = "http://127.0.0.1:8000/api/crud";
            await axios
                .get(url)
                .then((response) => {
                    this.products = response.data.data;
                    console.log(this.products);
                })
                .catch((error) => {
                    console.log(error);
                });
        },
        async delProduct(id) {
            let url = `http://127.0.0.1:8000/api/crud/${id}`;
            await axios
                .delete(url)
                .then((response) => {
                    if (response.data.code == 200) {
                        alert(response.data.message);
                        this.getProduct();
                    }
                })
                .catch((error) => {
                    console.log(error);
                });
        },
    },
    mounted() {
        console.log("product list created");
    },
};
</script>