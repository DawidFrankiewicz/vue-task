<script setup>
import ProductsGrid from "./ProductsGrid.vue";
import { ref, onMounted } from "vue";

const loadingUsers = ref(true);
const usersApiData = ref({});

onMounted(async () => {
	try {
		const response = await fetch("http://localhost:8082/products", {
			method: "GET",
			headers: {
				"Content-Type": "application/json",
			},
		});
		const json = await response.json();
		usersApiData.value = json;
		loadingUsers.value = false;
	} catch {
		console.error("Error fetching data");
	}
});
</script>

<template>
	<div v-if="loadingUsers" class="container">
		<h1>Wczytywanie produktów...</h1>
	</div>
	<div v-else class="products-app container">
		<h1>Produkty</h1>
		<ProductsGrid
			:products="usersApiData['best-sales'] ? usersApiData['best-sales'] : []"
		/>
	</div>
</template>

<style lang="scss" scoped></style>
