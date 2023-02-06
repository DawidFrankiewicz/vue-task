<script setup>
import { ref } from "vue";
const playAnimationOnAddToCart = ref(false);
const { product } = defineProps({
	product: {
		type: Object,
		required: true,
	},
});

const addToWishlist = () => {
	product["added-to-wishlist"] = !product["added-to-wishlist"];
};

const addToCart = () => {
	console.log(`Dodano do koszyka: ${product.name}`);
	playAnimationOnAddToCart.value = true;
	setTimeout(() => {
		playAnimationOnAddToCart.value = false;
	}, 1000);
};
</script>

<template>
	<div class="product-card">
		<div
			class="product-card__add-to-card-animation"
			:class="
				playAnimationOnAddToCart
					? 'product-card__add-to-card-animation--active'
					: null
			"
		>
			🛒
		</div>
		<div class="product-card__badges-container">
			<div
				v-if="product.badges.new"
				class="product-card__badge product-card__badge--new"
			>
				NOWY!
			</div>
			<div
				v-if="product.badges['collection-sale']"
				class="product-card__badge product-card__badge--collection-sale"
			>
				OSTATNIE SZTUKI
			</div>
			<div
				v-if="product.badges['last-items']"
				class="product-card__badge product-card__badge--last-items"
			>
				WYPRZEDAŻ KOLEKCJI
			</div>
		</div>
		<button
			@click="addToWishlist"
			class="product-card__add-to-wishlist"
			:class="product['added-to-wishlist'] ? 'wishlisted' : null"
		>
			❤
		</button>

		<img class="product-card__image" :src="product.image" alt="product image" />
		<div class="product-card__details">
			<div class="product-card__price-and-name">
				<h2>{{ product.name }}</h2>
				<p class="product-price-tag">
					<span
						v-if="product.price.regular !== product.price.current"
						class="product-price-tag__regular"
						>{{ product.price.regular }}zł</span
					>
					<span class="prodct-price-tag__current">
						{{ product.price.current }}zł</span
					>
				</p>
			</div>
			<button @click="addToCart">Dodaj do koszyka</button>
		</div>
	</div>
</template>

<style lang="scss" scoped>
@use "../assets/_variables.scss" as vars;
.product-card {
	display: flex;
	flex-direction: column;
	border: 1px solid vars.$color-tertiary-dark;
	box-shadow: 0 0 3px 1px vars.$color-tertiary-dark;
	border-radius: 8px;
	background-color: vars.$color-white;
	overflow: hidden;
	position: relative;
	cursor: pointer;
	&:hover {
		border: 1px solid vars.$color-primary;
		box-shadow: 0 0 3px 1px vars.$color-primary;
		h2 {
			color: vars.$color-primary;
		}
	}
}

.product-card__badges-container {
	position: absolute;
	top: 0;
	left: 0;
	display: flex;
	flex-direction: column;
}

.product-card__badge {
	background-color: vars.$color-black;
	color: vars.$color-white;
	padding: 0.5em 1em;
	font-weight: 700;
	font-size: 0.8rem;
	&--new {
		background-color: rgba(vars.$color-primary, 0.7);
	}
	&--collection-sale {
		background-color: rgba(vars.$color-tertiary, 0.7);
	}
	&--last-items {
		background-color: rgba(vars.$color-tertiary-dark, 0.7);
	}
	&:last-child {
		border-end-end-radius: 18px;
	}
}

.product-card__add-to-wishlist {
	position: absolute;
	top: 10px;
	right: 10px;
	font-size: 1.5rem;
	width: 35px;
	height: 35px;
	display: flex;
	border-radius: 10px;
	justify-content: center;
	align-items: center;
	padding: 0;
	color: vars.$color-tertiary;
	background-color: vars.$color-white;
	border: 0;
	cursor: pointer;
	&.wishlisted {
		color: vars.$color-primary;
		box-shadow: 0 0 3px 1px vars.$color-primary;
	}
	&:hover {
		color: vars.$color-tertiary-dark;
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
		font-size: 1.25rem;
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
	display: inline-block;
	background-color: rgba(vars.$color-tertiary-light, 0.4);
	border-radius: 5px;
	padding: 0.2em 0.5em;
}

.product-price-tag__regular {
	text-decoration: line-through;
	color: vars.$color-tertiary;
	font-size: 0.6em;
	margin-right: 0.3em;
}

@keyframes blink {
	0% {
		opacity: 0;
	}
	50% {
		opacity: 1;
	}
	100% {
		opacity: 0;
	}
}
.product-card__add-to-card-animation {
	position: absolute;
	top: 0;
	left: 0;
	width: 100%;
	height: 100%;
	display: flex;
	justify-content: center;
	align-items: center;
	font-size: 2rem;
	pointer-events: none;
	color: vars.$color-white;
	background-color: rgba(vars.$color-primary, 0.7);
	opacity: 0;
	&.product-card__add-to-card-animation--active {
		animation: blink 1s ease-in-out;
	}
}
</style>
