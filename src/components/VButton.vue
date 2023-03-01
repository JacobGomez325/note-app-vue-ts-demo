<template>
  <div>
		<button @click="$emit('click')" :class="bgColor" class="px-3 py-2 w-full  font-semibold uppercase shadow text-white">
			<slot></slot>
		</button>
  </div>
</template>

<script lang="ts" setup>
	import { PropType } from 'vue';
	const {bgColor} = defineProps({
		bgColor:{
			type:String as PropType<string>,
			required: true,
		}
	})
</script>

<style  scoped>

</style>