<script setup>
	import { ref, onMounted } from 'vue';

	const result = ref([]); // ✅ réactif et visible par le template
	const response = ref([]);
	const url = "http://192.168.1.189:3000/person";
	onMounted(async () => {
		try{
			const response = await fetch(url);

			if (!response.ok) {
				throw new Error(`Response status: ${response.status}`);
			}
			result.value = await response.json();
		} finally {
			console.error("finished");
		}
	})

</script>

<template>
	<a href="/details?uuid=75fd4e72-f902-4e2d-8f76-cfe41c183a8b" v-for="data in result" class="data-box aspect-9/16 border-blue-400 border-2 w-[19%] h-[50%] rounded-4xl grid grid-cols-1 grid-rows-2 p-3">
		<img src="/who.png" alt="" class="object-center border-blue-400 w-full h-full rounded-3xl">
		<div class="info overflow-auto contain-content grid grid-cols-2 text-center text-blue-500 items-center">
			<h1>Noms : {{ data.first }}</h1>
			<h1>Prenoms : {{ data.last }}</h1>
			<h1>Birth : {{ data.birth }}</h1>
			<h1>Gender : {{ data.gender }}</h1>
			<h1>Nationalities : {{ data.nationalities }}</h1>
			<h1>Origins : {{ data.origins }}</h1>
			<h1>Created_at : {{ data.created_at }}</h1>
			<h1>Updated_at : {{ data.updated_at }}</h1>
		</div>
	</a>
</template>

