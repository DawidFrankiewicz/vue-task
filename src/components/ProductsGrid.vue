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
		<ProductCard
			v-for="product in products"
			:key="product.name"
			:product="product"
		/>
	</div>
</template>

<style lang="scss" scoped>
.products-grid {
	display: grid;
	gap: 1rem;
	@media screen and (min-width: 450px) {
		grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
	}
}
</style>
