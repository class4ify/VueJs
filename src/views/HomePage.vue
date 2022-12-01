<template>
    <div class="container">
        <div class="mt-5">
  
            <div class="row d-flex justify-content-center">
                <div class="col-sm-3 ml-2 mr-4 mb-4" v-for="(category) in categorys" :key="category.id">
                    <div class="card-body" style="width: 18rem">
                        <a href="/" role="button">
                            <center>
                                <img :src="`http://127.0.0.1:8000/storage/${category.photo}`" height="210"
                                    class="card-img-top" />
                            </center>
                        </a>
                        <div class="card-body ">
                            <h5 class="card-title " align="center">{{ category.category }}</h5>
                            <div class="d-flex">
                            <router-link :to="{ name: 'filteredlist', params: { id: category.id } }"
                                class="ctn-del r ">Lihat Produk</router-link>
                            <!-- <button class="btn btn-outline-dark btn-sm rounded mr-4"
                                @click.prevent="delcategory(category.id)">Lihat Produk</button> -->
                            <button class="ctn-del hover-del"
                                @click.prevent="delcategory(category.id)">Delete</button>
                            </div>

                         
   

                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style>


@import url('https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap');


.hover-del:hover {
    color: red;
}

.r:hover {
    color: rgb(63, 206, 63) !important;
    text-decoration: none;
}

.text-btn {
    color: rgb(13, 110, 253) !important;
    background-color: white !important;
    font-family: 'Roboto Mono', monospace !important;
}

.text-btn:hover {
    color: white !important;
    background-color: rgb(13, 110, 253) !important;
    font-family: 'Roboto Mono', monospace !important;
}


.ctn-del {
    align-items: center;
    appearance: none;
    background-color: #FCFCFD;
    border-radius: 4px;
    border-width: 0;
    box-shadow: rgba(45, 35, 66, 0.4) 0 2px 4px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
    box-sizing: border-box;
    color: #36395A;
    cursor: pointer;
    display: inline-flex;
    font-family: "JetBrains Mono", monospace;
    height: 35px;
    justify-content: center;
    align-items: center;
    line-height: 1;
    list-style: none;
    overflow: hidden;
    padding-left: 16px;
    padding-right: 16px;
    position: relative;
    text-align: left;
    text-decoration: none;
    transition: box-shadow .15s, transform .15s;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
    white-space: nowrap;
    will-change: box-shadow, transform;
    font-size: 18px;
    margin-left: 17px;
}

.ctn-del:focus {
    box-shadow: #D6D6E7 0 0 0 1.5px inset, rgba(45, 35, 66, 0.4) 0 2px 4px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
}

.ctn-del:hover {
    box-shadow: rgba(45, 35, 66, 0.4) 0 4px 8px, rgba(45, 35, 66, 0.3) 0 7px 13px -3px, #D6D6E7 0 -3px 0 inset;
    transform: translateY(-2px);
}

.ctn-del:active {
    box-shadow: #D6D6E7 0 3px 7px inset;
    transform: translateY(2px);
}

.r {
    margin-left: -17px !important;
}

.hover-del {
    margin-right: -15px !important;
    margin-left: 30px !important;
}
</style>

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
                        // alert(response.data.message);
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
