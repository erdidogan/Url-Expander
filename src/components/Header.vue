<template>
    <section class="hero is-fullheight">
        <div class="hero-body">
            <div class="container has-text-centered">
            <Search/>
            </div>
        </div>
    <Footer/>
    </section>
</template>

<script>
    import Search from "./Search";
    import Footer from "@/components/Footer";
    export default {
        name: "Header",
        components: {Footer, Search}
    }
</script>

<style scoped>

</style>
