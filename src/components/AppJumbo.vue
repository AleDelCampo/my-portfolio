<script>
export default {
    name: 'AppFooter',
}

</script>

<template>
    <div class="container-fluid w-75 bg-jumbo rounded-3">
        <div class="jumbotron p-2 mb-4 bg-jumbo">
            <div class="container-fluid cnt">
                <h1 class="display-4 fw-bold">Welcome to my side!!</h1>
                <p class="col-md-8 fs-4">This is my little portfolio site, Work in Progress!!</p>
                <div>
                <router-link :class="my-btn" :to="{ name: 'contact-me' }" class="btn my-btn">Contact Me!!</router-link>
            </div>
            </div>
        </div>

    </div>
</template>

<style lang="scss" scoped>
div {
    color: black;
}

.cnt {
    height: 224px;
}

.bg-jumbo {
    background-color: #ad32ff;
}

.my-btn {
    border: 1px solid #fd2bfd;
    color: black;

    &:hover {
        background-color: transparent;
        color: white;
    }

}
</style>