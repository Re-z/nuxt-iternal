<template>
	<div class="galaxy">
		<div class="galaxies__col galaxies__col_name">
			<p class="galaxy__col-title galaxy__col-title_dark">Galaxy name</p>
			<figure class="galaxy__figure">
				<!-- img src prevents crushed imgs -->
				<img class="galaxy__img" :src="galaxy.img || imgFallback" alt="">
				<figcaption	class="galaxy__img-descr">{{galaxy.name}}</figcaption>
			</figure>
		</div>
		<div class="galaxies__col galaxies__col_constel">
			<p class="galaxy__col-title">Constellation</p>
			<p class="galaxy__text">{{galaxy.constellation}}</p>
		</div>
		<div class="galaxies__col galaxies__col_descr">
			<p class="galaxy__col-title">Origin of name	</p>
			<p class="galaxy__text">{{galaxy.originOfName}}</p>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			imgFallback: 'https://www.placecage.com/30/30'
		}
	},
	props: {
		galaxy: Object
	}
}
</script>