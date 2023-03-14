<script>
import { page } from '$app/stores';
import { onMount } from 'svelte';

$: id = $page.params.id;

let items = [];

onMount(async () => {
  const response = await fetch(`http://localhost:9000/board/${id}`);
  items = await response.json();
});

function gotoPage(direction) {
  const nextPageId = direction === 'next' ? +id + 1 : +id - 1;
  location.href = `/board/${nextPageId}`
}
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">

	{#if items.length === 0}
    <p>loading..</p>
  {:else}
    {#each items as item, index}
	  <div class="board">
		<p class="board__id">{item.id}</p>
		<h1 class="board__title">{item.title}</h1>
		
		<div class="board__content">
		  <p>{item.content}</p>
		</div>
		<div class="board__date">
		  <p>{new Date(item.create_date).toISOString().slice(0, 10)}</p>
		</div>
		<div class="board__button-group">
		  <button class="board__button" on:click={() => gotoPage('prev')} disabled={id <= 1}> 이전 페이지</button>
		  <button class="board__button" on:click={() => gotoPage('next')} disabled={id >= 50}> 다음 페이지</button>
		</div>
	  </div>
    {/each}
  {/if}
</div>
