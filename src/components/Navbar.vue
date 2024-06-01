<template>
    <div class="navi">
        <nav>
        <h2>DAFTAR BUKU</h2>
        <ul>
            <li><a href="#Main">HOME</a></li>
            <li><a href="#Buku">BUKU</a></li>
        </ul>
        </nav> 
    </div>
</template>

<style>
.navi{
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    background: #e48d85;
    z-index: 1000;
}

nav{
    display: flex;
    width: 100%;
    padding: 20px 0;
    align-items: center;
    justify-content: space-between;
    margin: 0;
}

nav ul li{
    display: inline-block;
    list-style: none;
    margin: 10px 20px;
}

nav ul li a{
    text-decoration: none;
    color: #a23c33;
    font-weight: bold;
}

nav ul li a:hover{
    color: #df5430;
}

h2{
    margin: 0 20px 0 20px;
    color: #a23c33;
    font-weight: bold;
}
</style>