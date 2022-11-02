<template>
    <div class="container">
        <div class="row mt-4">
            <div class="col">
                <router-link to="/add" type="submit" class="btn"
                    style="float: right; background-color: #4C566A; color:white">Tambah Product</router-link>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div class="card" style="width: 18rem">
                    <!-- <img class="card-img-top" src="/Users/PC-TKJ/Downloads/download (1).jpg" alt="Card image cap" /> -->
                    <div class="card-body">
                        <h5 class="card-title">Card title</h5>
                        <p class="card-text">Some quick example text to build on the card title</p>
                        <button href="#" class="btn bordered" style="background-color: #4C566A; color:white">Go
                            somewhere</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style>
.router-link-active {
    font-weight: bolder;
    font-size: larger;
    /* font-style: italic; */
}
</style>