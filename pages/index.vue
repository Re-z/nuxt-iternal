<template>
	<main class="content">
		<div class="heading">
			<div class="heading__left">
				<h1 class="page-title">Named galaxies</h1>
			</div>
			<div class="heading__right">
				<div class="input-wrap has-icon-search">
					<input
						class="input-wrap__input"
						type="text"
						v-model="search"
						placeholder="Search galaxies"
						>
				</div>
			</div>
		</div>

		<div class="galaxies">
			<div class="galaxies__heading">
				<div 
					class="galaxies__col galaxies__col_name"
					@click="sortGalaxiesByName"
					>
					<span 
						class="galaxies__heading-text galaxies__heading-text_bold"
						:class="{'sortedZA': !this.sortAZ}"
						>Galaxy Name</span>
				</div>
				<div class="galaxies__col galaxies__col_constel">
					<span class="galaxies__heading-text">Constellation</span>
				</div>
				<div class="galaxies__col galaxies__col_descr">
					<span class="galaxies__heading-text">Origin of name</span>
				</div>
			</div>
			<div class="galaxies__content">
				<Galaxy
					v-for="galaxy in galaxiesInDOM"
					:key="galaxy.id"
					:galaxy="galaxy"
				/>

			</div>
		</div>
	</main>
</template>

<script>
import Galaxy from '@/components/Galaxy.vue'
export default {
	data() {
		return {
			search: '',
			galaxiesInDOM: [],
			allGalaxies: [],
			sortAZ: false //if true -from A to Z sorting, false - from Z to A
		}
	},
	methods: {
		getDataFromAPI() {
			const url = 'https://cors-anywhere.herokuapp.com/https://test-frontend-api.herokuapp.com/galaxies'
			fetch(url)
				.then(response => response.json())
				.then(data => { this.allGalaxies = data })
				.then(data => { this.filterGalaxiesByName() })
				.then(data => { this.sortGalaxiesByName() })
		},
		filterGalaxiesByName() {
			this.galaxiesInDOM = this.allGalaxies.filter(galaxy => {
				if(galaxy.name.toLowerCase().includes(this.search.toLowerCase())) {
					return galaxy;
				}
			})
		},
		sortGalaxiesByName() {
			this.galaxiesInDOM.sort((a, b) => {
				if(this.sortAZ) {
	    			return b.name.localeCompare(a.name);
				} 
				else {
	    			return a.name.localeCompare(b.name);
				}
			  });
			this.sortAZ = !this.sortAZ;
		}
	},
	watch: {
		search() {
			this.filterGalaxiesByName();
		}
	},
	mounted() {
		this.getDataFromAPI();
	},
	components: {
		Galaxy
	}
}
</script>