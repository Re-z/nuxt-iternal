<template>
	<div class="has-sidebar">
		<div class="has-sidebar__left">
			<Sidebar/>
		</div>

		<div class="has-sidebar__right">
			
			<nuxt/>
		</div>
		

	</div>
		
</template>


<script>
import Sidebar from '@/components/Sidebar.vue'
export default {
	components: {
		Sidebar
	}
}
</script>