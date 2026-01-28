<script setup>
	import { ref, onMounted } from 'vue';
import { errorMessages } from 'vue/compiler-sfc';

	const result = ref([]); // ✅ réactif et visible par le template

	const url = "http://192.168.1.189:3000/person";
	try{
		const response = await fetch(url);
		const result = respons.data;
	} catch (!response.ok) {
		console.error("error");
	} finally {
		console.error("finished");
	}
</script>

<template>
	<div v-for="data in result" :key="data.id" class="data-box border-blue-400 border-2 w-[19%] h-[50%] rounded-4xl grid grid-cols-1 grid-rows-2 p-3">
	<img src="/image.png" alt="" class="object-center border-blue-400 w-full h-full rounded-3xl">
	<div class="info grid gap-1 grid-cols-2 text-center text-blue-500 items-center">
		<h1>Noms : {{ data.first }}</h1>
		<h1>Prenoms : {{ data.last }}</h1>
		<h1>Birth : {{ data.birth }}</h1>
		<h1>Gender : {{ data.gender }}</h1>
		<h1>Nationalities : {{ data.nationalities }}</h1>
		<h1>Origins : {{ data.origins }}</h1>
		<h1>Created_at : {{ data.created_at }}</h1>
		<h1>Updated_at : {{ data.updated_at }}</h1>
	</div>
	</div>
</template>
