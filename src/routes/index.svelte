<script context="module">
	export function preload({ params, query }) {
		return this.fetch(`index.json`).then(r => r.json()).then(posts => {
			return { posts };
		});
	}
</script>

<script>
	export let posts;

	import _ from 'lodash';
	import Post from "./_post.svelte";
	import Feature from "./_feature.svelte";

	let filter = '';
	let feature = 'PopCare';
</script>

<style>
	[sticky]{
		position:sticky;
		top:0;
	}
</style>

<svelte:head>
	<title>Emergency FYI</title>
</svelte:head>


<section p="8 sm3" bg="gray3">
  <ul grid columns="3" gap="6">
    <li cell span="3">
			<h1>Emergency FYI for COVID-19</h1>
    </li>
    <li cell>
      <h2>
        Find help in your community.
      </h2>
      <p>The COVID-19 pandemic is overwhelming federal, state, and local capacities of the United States government. We can help you find resources and aid in your local area to navigate this ongoing crisis, and expand your network for volunteer work.</p>
    </li>
  </ul>
</section>

<div alert type="alert" color="white" class="h3" flex px="8 sm3" align="center" py="4"><span>We have 2 weeks to slow the spread of Coronavirus. Start by following the <a color="white" class="hide" href="https://www.coronavirus.gov/">US Government</a> response.</span><a button ml="4" class="hide" href="https://www.coronavirus.gov/">coronavirus.gov</a></div>

<section p="8 sm3">
	<ul grid columns="3" gap="6">
		<li cell bg="gray1">
			<h3>Listed are active efforts to mitigate the worst effects of COVID-19.</h3>
			<fieldset>
				<label>Search by topic:</label>
				<input bind:value={filter} placeholder="Filter">
			</fieldset>
			<h3>If this is an emergency, contact your local health department.</h3>
			<a button href="/health-depts" mb="3">Health Departments</a>
		</li>
		{#each posts as post}
			{#if _.some(post.tags, tag => (tag.match(filter))) }
				<Post {post} />
			{/if}
		{/each}
	</ul>
</section>