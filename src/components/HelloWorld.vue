<script setup>
defineProps({
	msg: {
		type: String,
		required: true,
	},
});
</script>

<template>
	<div class="container">
		<h1 class="green">
			{{ msg }}
		</h1>
	</div>
</template>

<style lang="scss" scoped>
@use "../assets/_variables.scss" as vars;
h1 {
	color: vars.$color-black;
	font-weight: 500;
	font-size: 2.6rem;
	top: -10px;
	text-align: center;
	@media (min-width: 1024px) {
		text-align: left;
	}
}
</style>
