<script>
	import '$styles/app.css'
	import Meta from '$components/Meta.svelte'

	// FIXME: FOUC, namely the font loading
	import { onMount } from 'svelte' // goes away in Svelte 5?
	import Hamburger from '$components/Hamburger.svelte'
	import Header from '$components/Header.svelte'
	import Works from '$components/Works.svelte'
	import Footer from '$components/Footer.svelte'
	import Spacer from '$components/Spacer.svelte'
	import { numVisits } from '$stores/localStorage.js'
	import data from '$lib/assets/works.json' //in lieu of reading data in - this is the data driven part 8)
<<<<<<< HEAD
	let open = false

	function groupBy(data, key) {
		return data.reduce((acc, cur) => {
			acc[cur[key]] = acc[cur[key]] || []
			// if the key is new, initialize its value to an array,
			// otherwise keep its own array value
			acc[cur[key]].push(cur)
			return acc
		}, [])
	}
=======
	import { group } from 'd3' // used to group data based upon the 'type' of card; use until Object.groupBy or Map.groupBy happens.
	let open = false

>>>>>>> 7c7c5b3 (open-props with d3 groupby)
	// Update number of user visits
	$numVisits += 1 //  browser persistent local storage
	// FIXME: Can this be done elsewhere for optimization?
	// Process data
<<<<<<< HEAD
	const groupedData = groupBy(data, 'type')

=======
	const groupedData = group(data, (d) => d.type) // aggregate based upon the 'type' of card
	
>>>>>>> 7c7c5b3 (open-props with d3 groupby)
	onMount(() => {
		// after the DOM loads, animate the cards once. Love greensock.
		// To do: animate as user scrolls down the page using gsap's ScrollTrigger
		// runAnimations()
	})

	// // there are two steps to add a new section: 1) add to the types array
	const types = ['stories', 'viz', 'miscellanea', 'papers', 'billweek'] // these are the sections for the cards as specified in the works.js file

<<<<<<< HEAD
	// candidate for a loop if we did this: //
=======
>>>>>>> 7c7c5b3 (open-props with d3 groupby)
	const category = {
		stories: 'data stories',
		viz: 'data visualizations',
		miscellanea: 'miscellanea',
		papers: 'technical papers',
		billweek: 'Bill Week'
	}

	let keys = Object.keys(category)
</script>

<!-- load metadata -->
<Meta />

<div class="wrapper">
	<Header />
	<main>
		<!-- there are two steps to add a new section: this is 2) add a new <Works /> <Spacer /> unit
			As content grows, we will need to be aware of performance issues as there are a lot of images being loaded
		 -->

		{#each keys as key}
<<<<<<< HEAD
			<Works type={category[key]} id={key} data={groupedData[key]} />
=======
			<Works type={category[key]} id={key} data={groupedData.get(key)} />
>>>>>>> 7c7c5b3 (open-props with d3 groupby)
			<Spacer />
		{/each}
		<!-- <Works type={'data stories'} id={'stories'} data={groupedData.get('stories')} />
		<Spacer />
		<Works type={'data stories'} id={'stories'} data={groupedData.get('stories')} />
		<Spacer />
		<Works type={'data visualizations'} id={'viz'} data={groupedData.get('viz')} />
		<Spacer />
		<Works type={'miscellanea'} id={'miscellanea'} data={groupedData.get('miscellanea')} />
		<Spacer />
		<Works type={'technical papers'} id={'papers'} data={groupedData.get('papers')} />
		<Spacer />
		<Works type={'Bill Week'} id={'billweek'} data={groupedData.get('billweek')} /> -->
		<Spacer />
	</main>
	<Footer />
</div>
<Hamburger bind:open />

<style>
	.wrapper {
		min-height: 100%;
		display: flex;
		flex-direction: column;
	}
</style>
