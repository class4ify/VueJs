<template>
    <html lang="en">

    <head>
        <meta charset="utf-8">
        <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

        <!-- Bootstrap CSS -->
        <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/bootstrap@4.6.2/dist/css/bootstrap.min.css"
            integrity="sha384-xOolHFLEh07PJGoPkLv1IbcEPTNtaed2xpHsD9ESMhqIYd0nLMwNLD69Npy4HI+N" crossorigin="anonymous">



    </head>

    <body>
        <div id="nav-scroll">
            <nav class="navbar navbar-expand-lg navbar-light">
                <div class="container">
                    <a class=" navbar-brand" href="#">
                        <img src="../assets/logo.png" width="50x" height="50px">
                    </a>
                    <a class="navbar-brand" href="/">Vue.js</a>
                    <button class="navbar-toggler" type="button" data-toggle="collapse"
                        data-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false"
                        aria-label="Toggle navigation">
                        <span class="navbar-toggler-icon"></span>
                    </button>
                    <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
                        <ul class="navbar-nav">
                            <li class="nav-item">
                                <router-link class="nav-link" to="/">Home</router-link>
                            </li>
                            <li class="nav-item">
                                <router-link class="nav-link" to="/list">List Product</router-link>
                            </li>
                            <li class="nav-item dropdown">
                                <a class="nav-link dropdown-toggle" role="button" data-bs-toggle="dropdown"
                                    aria-expanded="false">
                                    Add
                                </a>
                                <ul class="dropdown-menu">
                                    <li><router-link class="dropdown-item" to="/add">Tambah Produk</router-link></li>
                                    <li><router-link class="dropdown-item" to="/addC">Tambah Kategori</router-link></li>
                          
                                </ul>
                            </li>
                        </ul>



                    </div>
                </div>
            </nav>
        </div>
    </body>

    </html>
</template>
<script>
name: "NavBar"
</script>
    
    
    
<style>
body,
html {
    margin: 0;
    padding: 0;
    scroll-behavior: smooth;
    font-family: Arial, Helvetica, sans-serif;
    /* overflow-x: hidden; */
    /* border: 5px solid black; */
}

.navbar-nav {
    margin-left: auto;
}

#nav-scroll {
    /* position: fixed; */
    top: 0;
    width: 100%;
    background-color: white;
    border-bottom: 3px solid gray;
    z-index: 111;
    border-bottom-color: rgba(128, 128, 128, 0.2);
    transition: top 0.3s;
    /* text-transform: uppercase; */
    font-weight: 600;

}

.nav-link:hover {
    /* content: ""; */
    /* display: block; */
    border-bottom: 3px solid gray;
    width: 100%;
    margin: auto;
    padding-bottom: 5px;
    margin-bottom: -8px;
}
</style>