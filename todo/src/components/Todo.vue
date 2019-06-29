<template>
	<div class="title flex-centered" :class="{checked: todo.checked}">
		<div class="title-icon">
			<i class="icon" :class="todo.checked ?'icon-check' : 'icon-time'"></i>
		</div>
		<dir class="title-content">
			<div class="title-subtitle">{{ todo.description }}</div>
		</dir>
		<div class="title-action">
			<button @click="$emit('toggle', todo)" class="btn btn-link">
				<span v-if="todo.checked">mark off</span>
				<span v-else>done</span>
			</button>
			<button @click="$emit('remove', todo)" class="btn btn-link">
				<span class="text-error">remove</span>
			</button>
		</div>
	</div>
</template>

<script>
	export default{
		props:{
			todo: {type: Object, required: true}
		}
	}
</script>

<style scoped>
.checked{
	text-decoration: line-through;
	color: rgb(108, 179, 151);
}
</style>
