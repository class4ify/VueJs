<template>
    <div class="container">
        <div class="card mt-5 mt-4">
            <div class="card-body mx-4">
                <div class="row ">
                    <div class="col">
                        <h4>
                            <span class="badge mx-5" style="background-color: #4C566A;">Ubah Data Product</span>
                        </h4>
                    </div>
                </div>
                <div class="row mt-2">
                    <div class="col p-4">
                        <form @submit.prevent="updateproduct">
                            <div class="form-group row px-5">
                                <label class="col-sm-2 col-form-label  ">Nama Pesanan</label>
                                <input type="text" class="form-control bordered" v-model="products.title" />
                            </div>
                            <div class="form-group row px-5 ">
                                <label class="col-sm-2 col-form-label">Harga Pesanan</label>
                                <input type="number" class="form-control" v-model="products.price" />
                            </div>
                            <div class="form-group row px-5">
                                <label class="col-sm-2 col-form-label">Kategori</label>
                                <select class="custom-select form-control" id="inputGroupSelect03"
                                v-model="products.category" placeholder="...">
                                <option v-for="(category) in categorys" 
                                :value="category.id"
                                :key="category">
                                {{ category.category }}</option>
                            </select>
                            </div>
                            <div class="form-group px-5 row ">
                                <label class="form-label mt-4">Gambar Pesanan</label>
                                <input class="form-control" type="file" @change="imgupload" />
                                <input class="form-control" type="text" v-model="products.image" />
                            </div>
                            <div class="form-group mt-4 ml-4">
                                <img :src="preview" alt="" width="200" />
                            </div>
                            <button type="submit" class="btn mx-4"
                                style="float: right; background-color: #4C566A; color: white;">Submit</button>
                        </form>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<!-- a -->
<script>
import axios from "axios";
export default {
    name: "editpage",
    data() {
        return {
            categorys: Array,
            
            products: {},
            image: '',
            preview: '',
        }
    },
    created() {
        this.getProductById();
        this.getCategory();
    },
    methods: {
        async getProductById() {
            let url = `http://127.0.0.1:8000/api/crud/${this.$route.params.id}`;
            await axios.get(url).then(response => {
                // console.log(response);
                this.products = response.data.data;
            })
                .catch(error => {
                    // console.log(errorf);
                });
        },
        imgupload(e) {
            this.image = e.target.files[0];
            // console.log(this.image);

            const fileName = e.target.files[0].name;

            this.products.image = fileName;

            let fileReader = new FileReader();
            fileReader.readAsDataURL(this.image);
            fileReader.onloadend = e => {
                this.preview = e.target.result;
                // console.log(this.preview);
            }
        },
        async updateproduct() {
            let title       = this.products.title;
            let price       = this.products.price;
            let image       = this.products.image;
            let category    = this.products.category;
            // console.log(title);
            // console.log(price);
            // console.log(image);

            axios.put(`http://127.0.0.1:8000/api/crud/${this.$route.params.id}`
                , {
                    title: title,
                    price: price,
                    image: image,
                    category_id: category,
                })
                .then((response) => {
                    // console.log(response);
                    this.$router.push({ name: 'listpage' });
                })
                .catch(error => {
                    // console.log(error);
                });

        },
        async getCategory() {
            let url = "http://127.0.0.1:8000/api/category";
            await axios
                .get(url)
                .then((response) => {
                    this.categorys = response.data.data;
                    console.log(this.products);
                })
                .catch((error) => {
                    console.log(error);
                });
        },

    },
};
</script>

