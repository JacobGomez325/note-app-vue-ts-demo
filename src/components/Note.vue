<template>
  <div :style="`background-color:${note.color}`" class="h-60 w-60 flex flex-col overflow-hidden justify-between p-1 shadow rounded-sm ">
		<div class="w-full">
			<h3 class="text-xl font-bold py-2 uppercase"> {{ note.title }} </h3>
			<p class="text-md font-semibold ">{{ note.content }}</p>
		</div>
		<div class="flex justify-between">
			<p class="text-md font-bold"> {{ note.date.toLocaleDateString() }} </p>
			<p class="flex space-x-2">
				<span title="modifier" @click="updateData(note)" class="cursor-pointer text-blue-500"><svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24" height="1.3em" width="1.3em" xmlns="http://www.w3.org/2000/svg"><path d="m7 17.013 4.413-.015 9.632-9.54c.378-.378.586-.88.586-1.414s-.208-1.036-.586-1.414l-1.586-1.586c-.756-.756-2.075-.752-2.825-.003L7 12.583v4.43zM18.045 4.458l1.589 1.583-1.597 1.582-1.586-1.585 1.594-1.58zM9 13.417l6.03-5.973 1.586 1.586-6.029 5.971L9 15.006v-1.589z"></path><path d="M5 21h14c1.103 0 2-.897 2-2v-8.668l-2 2V19H8.158c-.026 0-.053.01-.079.01-.033 0-.066-.009-.1-.01H5V5h6.847l2-2H5c-1.103 0-2 .897-2 2v14c0 1.103.897 2 2 2z"></path></svg></span>
				<span title="supprimer" @click="deleteData(note)" class="cursor-pointer text-red-500"><svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 24 24" height="1.3em" width="1.3em" xmlns="http://www.w3.org/2000/svg"><path fill="none" d="M0 0h24v24H0z"></path><path d="M6 19c0 1.1.9 2 2 2h8c1.1 0 2-.9 2-2V7H6v12zM19 4h-3.5l-1-1h-5l-1 1H5v2h14V4z"></path></svg></span>
			</p>
		</div>
  </div>
</template>

<script lang="ts" setup>
	//les imports 

	import { PropType } from "vue";
	import Note from "../types/note.interface"
	
	// les macros
	const {note} = defineProps(
		{
			note:{
				type: Object as PropType<Note>,
				required: true
			}
		}
	)
	const emit = defineEmits(['modifier','supprimer'])

	// les datas



	// les methodes 

	const updateData = (data:Note) => {
		emit('modifier',data)
	}
	const deleteData = (data:Note) => {
		
		emit('supprimer',data)
	}
</script>

<style  scoped>

</style><!--  -->