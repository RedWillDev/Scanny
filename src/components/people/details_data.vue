<script setup>
	import { ref, onMounted, defineProps } from 'vue';

	const result = ref([]); // ✅ réactif et visible par le template
	const response = ref([]);
  const props = defineProps({
    uuid: String
  });
  console.log("ID reçu dans Vue:", props.uuid);
	const url = `http://192.168.1.189:3000/person?uuid=eq.${props.uuid}`;
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
  <div class="profile-up flex w-full bg-[url(/home/red/Scanny/public/world.svg)] h-[35%] border-blue-500 border-solid border-b-4 items-end ">
    <img src="/home/red/Scanny/public/user-circle-o-svgrepo-com.svg" alt="" class="flex h-[60%] w-[15%] object-contain bg-amber-200 ml-[20%] ">
    <h1 class=""> {{ result[0]?.first }} {{ result[0]?.second }} {{ result[0]?.last }} </h1>
  </div>
  <div class="flex h-full justify-center p-1.5">
    <div class="grid grid-cols-2 grid-rows-6 h-full w-[97%] gap-3 ">
      <div class="data-square flex justify-center items-center">
        <div class="h-[95%] w-[95%]">
          <div>
            <h1 class=" ">Identité : </h1>
            <h1>
              Date de Naissance : {{ result[0]?.birth }} {{ props.id }}
            </h1>
            <h1>
              Genre : {{ result[0]?.gender }}
            </h1>
            <h1>
              Nationalités : {{ result[0]?.nationalities }}
            </h1>
            <h1>
              Origine : {{ result[0]?.origins }}
            </h1>
          </div>
        </div>
      </div>
      <div class="data-square flex justify-center items-center"> 
        <div class="h-[95%] w-[95%]">
          <h1>Bank</h1>
        </div>
      </div>
      <div class="data-square flex justify-center items-center">
        <div class="h-[95%] w-[95%]">
					<h1> Sites </h1>
        </div>
      </div>
      <div class="data-square flex justify-center items-center ">
        <div class="h-[95%] w-[95%]">
          
        </div>
      </div>
      <div class="data-square"></div>
      <div class="data-square"></div>
    </div>
  </div>
</template>

<style>
  .data-square{
    border: solid;
    border-radius: 20px;
    border-color: #3b82f6;

  }

  h1{
    color: #3b82f6;
    font-size: small;
  }

</style>