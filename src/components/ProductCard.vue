<script setup>
const { product } = defineProps({
	product: {
		type: Object,
		required: true,
	},
});
</script>

<template>
	<div class="product-card">
		<img class="product-card__image" :src="product.image" alt="product image" />
		<div class="product-card__details">
			<div class="product-card__price-and-name">
				<h2>{{ product.name }}</h2>
				<p class="product-price-tag">{{ product.price.regular }}zł</p>
			</div>
		</div>
	</div>
</template>

<style lang="scss" scoped>
@use "../assets/_variables.scss" as vars;
.product-card {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
	border: 1px solid vars.$color-tertiary-dark;
	box-shadow: 0 0 3px 1px vars.$color-tertiary-dark;
	border-radius: 8px;
	background-color: vars.$color-white;
	overflow: hidden;
	cursor: pointer;
	&:hover {
		border: 1px solid vars.$color-primary;
		box-shadow: 0 0 3px 1px vars.$color-primary;
		h2 {
			color: vars.$color-primary;
		}
	}
}

.product-card__details {
	display: flex;
	flex-direction: column;
	width: 100%;
	padding: 1em 1em;
	gap: 1em;
	h2,
	p {
		margin: 0;
	}
	h2 {
		color: vars.$color-tertiary;
	}
}

.product-card__price-and-name {
	display: flex;
	justify-content: space-between;
	align-items: center;
	gap: 1em;
}
.product-card__image {
	width: 100%;
	height: 200px;
	object-fit: cover;
}

.product-price-tag {
	color: vars.$color-primary;
	font-weight: 700;
	font-size: 1.2rem;
}
</style>
