<template>
    <div class="container">
        <div class="card mt-5 mt-4">
            <div class="card-body mx-4">
                <div class="row ">
                    <div class="col">
                        <h4>
                            <span class="badge mx-5" style="background-color: #4C566A;">Tambah Kategori</span>
                        </h4>
                    </div>
                </div>
                <div class="row mt-2">
                    <div class="col p-4">
                        <form @submit.prevent="savecategory">
                            <!-- <div class="form-group row px-5">
                                <label class="col-sm-2 col-form-label  ">Nama Pesanan</label>
                                <input type="text" class="form-control bordered" v-model="products.title" />
                            </div>
                            <div class="form-group row px-5 ">
                                <label class="col-sm-2 col-form-label">Harga Pesanan</label>
                                <input type="number" class="form-control" v-model="products.price" />
                            </div> -->
                            <div class="form-group row px-5">
                                <label class="col-sm-2 col-form-label">Kategori</label>
                                <input type="text" list="programmingLanguages" class="form-control bordered" v-model="categorys.category" />
                                <datalist id="programmingLanguages">
                                    <option value="Makanan"     >Makanan</option>
                                    <option value="Minuman"     >Minuman</option>
                                    <option value="Permen"      >Permen</option>
                                    <option value="Ice Cream"   >Ice Cream</option>
                                    <option value="Dessert"     >Dessert</option>
                                </datalist>
                            </div>
                            <div class="form-group px-5 row ">
                                <label class="form-label mt-4">Gambar Kategori</label>
                                <input class="form-control" type="file" @change="imgupload" />
                            </div>

                            <div class="form-group mt-4 ml-5">
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

<script>
import axios from "axios";
export default {

    name: "inputcategory",
    data() {
        return {
            categorys: {},
            photo: "",
            preview: ''
        };
    },

    methods: {
        imgupload(e) {

            //console.log(e.target.files[0]);
            this.photo = e.target.files[0];
            // console.log(this.image);

            // console.log(this.products.title);
            // console.log(this.products.price);

            let fileReader = new FileReader();
            fileReader.readAsDataURL(this.photo);
            fileReader.onload = (e) => {
                this.preview = e.target.result;
                // console.log(this.preview);
            };
        },
        async savecategory() {
            let formData = new FormData();
            // formData.append("title", this.products.title);
            // formData.append("price", this.products.price);
            formData.append("photo", this.photo);
            formData.append("category", this.categorys.category);
            // a
            // console.log(formData);

            let url = "http://127.0.0.1:8000/api/category";
            await axios
                .post(url, formData)
                .then((response) => {
                    if (response.data.success == true) {
                        // alert(response.data.message);
                        // this.products.title = "";
                        // this.products.price = "";
                        this.photo = "";
                        this.categorys.category = "";
                        this.preview = "";
                    }
                })
                .then((response) => {
                    // console.log(response);
                    this.$router.push({ name: 'inputcategory' });
                })
                .catch((error) => {
                    // console.log("penyimpanan gagal");
                });
        },
    },
};


</script>