<template>
    <div class="container">
        <div class="mt-5">


            <div class="row d-flex justify-content-center">
                <div class="col-sm-3 ml-2 mr-4 mb-4" v-for="(category) in categorys" :key="category.id">
                    <div class="card-body" style="width: 18rem">
                        <a href="/list" role="button">
                            <center>
                                <img :src="`http://127.0.0.1:8000/storage/${category.photo}`" height="210"
                                    class="card-img-top" />
                            </center>
                        </a>
                        <div class="card-body ">
                            <h5 class="card-title " align="center">{{ category.category }}</h5>

                            <router-link :to="{ name: 'filteredlist', params: { id: category.id } }"
                                class="btn btn-outline-dark btn-sm rounded mr-4">Lihat Produk</router-link>
                            <!-- <button class="btn btn-outline-dark btn-sm rounded mr-4"
                                @click.prevent="delcategory(category.id)">Lihat Produk</button> -->
                            <button class="btn btn-outline-danger btn-sm rounded"
                                @click.prevent="delcategory(category.id)">Delete</button>
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
            categorys: Array,
        };
    },
    created() {
        this.getcategory();
    },
    methods: {
        async getcategory() {
            let url = "http://127.0.0.1:8000/api/category";
            await axios
                .get(url)
                .then((response) => {
                    this.categorys = response.data.data;
                    // console.log(this.categorys);
                })
                .catch((error) => {
                    // console.log(error);
                });
        },
        async delcategory(id) {
            let url = `http://127.0.0.1:8000/api/category/${id}`;
            await axios
                .delete(url)
                .then((response) => {
                    if (response.data.code == 200) {
                        alert(response.data.message);
                        this.getcategory();
                    }
                })
                .catch((error) => {
                    // console.log(error);
                });
        },
    },
    mounted() {
        // console.log("category list created");
    },
};
</script>
