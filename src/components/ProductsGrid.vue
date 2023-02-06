<script setup>
import ProductCard from "./ProductCard.vue";
const { products } = defineProps({
	products: {
		type: Array,
		required: true,
	},
});
</script>

<template>
	<div v-if="products" class="products-grid">
		<template v-for="product in products">
			<ProductCard :product="product" />
		</template>
	</div>
</template>

<style lang="scss" scoped>
@use "../assets/_variables.scss" as vars;
.products-grid {
	display: grid;
	grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
	gap: 1rem;
}
</style>
