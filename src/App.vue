<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import ProductsApp from "./components/ProductsApp.vue";
</script>

<template>
	<header>
		<HelloWorld msg="Vue Task - Dawid Frankiewicz" />
	</header>

	<main>
		<ProductsApp />
	</main>
</template>

<style lang="scss">
@use "./assets/_variables.scss" as vars;
</style>
