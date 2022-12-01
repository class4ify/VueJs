<template>
    <div class="container">
        <div class="mt-5">
            <div class="judul1">
                <h5 class="text-center mb-5">List Product</h5>
            </div>

            <!-- <div class="judul2">
                <h5 class="text-center mb-5">Minuman</h5>
            </div> -->

            <div class="row d-flex justify-content-center">
                <div class="col-sm-3 ml-2 mr-4 mb-4" v-for="(product) in products" :key="product">
                    <div class="card" style="width: 18rem">
                        <center>
                            <img :src="`http://127.0.0.1:8000/storage/${product.image}`" height="210"
                                class="card-img-top" />
                        </center>
                        <div class="card-body ">
                            <h5 class="card-title ">{{ product.title }}</h5>
                            <p class="card-text">Harga Rp.{{ product.price }}</p>
                            <router-link class="btn btn-outline-primary btn-sm rounded "
                                :to="{ name: 'editpage', params: { id: product.id } }">Edit</router-link>&nbsp;

                            <button class="btn btn-outline-danger btn-sm rounded "
                                @click.prevent="delProduct(product.id)">Delete</button>
                        </div>
                    </div>
                </div>
            </div>

            <!-- <div class="judul3">
                <h5 class="text-center mb-5">Cemilan</h5>
            </div> -->
          
        </div>
    </div>

</template>

<style>
.judul3 h5 {
    content: "";
    display: block;
    border-bottom: 3px solid gray;
    width: 15%;
    margin: auto;
    padding-bottom: 5px;
    margin-bottom: -8px;
}

.judul2 h5 {
    content: "";
    display: block;
    border-bottom: 3px solid gray;
    width: 15%;
    margin: auto;
    padding-bottom: 5px;
    margin-bottom: -8px;
}

.judul1 h5 {
    content: "";
    display: block;
    border-bottom: 3px solid gray;
    width: 15%;
    margin: auto;
    padding-bottom: 5px;
    margin-bottom: -8px;
}
</style>

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
                    // console.log(this.products);
                })
                .catch((error) => {
                    // console.log(error);
                });
        },
        async delProduct(id) {
            let url = `http://127.0.0.1:8000/api/crud/${id}`;
            await axios
                .delete(url)
                .then((response) => {
                    if (response.data.code == 200) {
                        // alert(response.data.message);
                        this.getProduct();
                    }
                })
                .catch((error) => {
                    // console.log(error);
                });
        },
    },
    mounted() {
        // console.log("product list created");
    },
};
</script>