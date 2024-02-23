<style>
	.loading {
		display: flex;
		justify-content: center;
		align-items: center;
		height: 100vh;
		width: 100vw;
		position: absolute;
	}
</style>

<script lang="ts">
	import Avatar from "$lib/components/ui/Avatar/Avatar.svelte";
	import Button from "$lib/components/ui/Button/Button.svelte";
	import { axios } from "$lib/utils/axios.utils";

	async function loadPage() {
		const { data } = await axios.get("/users");
		return data;
	}

	const load = loadPage();
</script>

{#await load}
	<div class="loading">
		<h1>Loading...</h1>
	</div>
{:then data}
	<h1>Hi there {data.email}</h1>
	<hr />
	<table>
		<thead>
			<th>ID</th>
			<th>Email</th>
			<th>Created Date</th>
		</thead>
		<tbody class="divide-y">
			{#each data as item, i}
				<tr>
					<td>{i}</td>
					<td>{item.email}</td>
					<td>{new Date(item.createdAt).toLocaleDateString()}</td>
				</tr>
			{/each}
		</tbody>
	</table>
{/await}
