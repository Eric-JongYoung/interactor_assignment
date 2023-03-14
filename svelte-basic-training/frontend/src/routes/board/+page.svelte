<script>
	import { onMount } from "svelte";
	let my = []; // 빈 배열로 초기화
	let currentPage = 1;
	let itemsPerPage = 10; // 페이지 당 아이템 수
	let totalPages = 0;

	// ajax
	
	const fetchData = async () => {
		const response = await fetch(`http://localhost:8000/board/list`);
		const data = await response.json();
		my = data;
		totalPages = Math.ceil(my.length / itemsPerPage);
	};

	onMount(fetchData); // 컴포넌트가 마운트될 때 데이터를 가져옴

	function setPage(page) {
		 currentPage = page;

	}

	function getPaginatedItems(now) {
		const startIndex = (now - 1) * itemsPerPage;
		const endIndex = startIndex + itemsPerPage;
		return my.slice(startIndex, endIndex);
	}

	function getPages() {
		const pages = [];
		for (let i = 1; i <= totalPages; i++) {
			pages.push(i);
		}
		return pages;
	}
	function changePage(next){
		if(next==1){
			currentPage ++;
		}else{
			currentPage --;
		}
	}
</script>

<svelte:head>
	<title>About</title>
	<meta name="description" content="About this app" />
</svelte:head>

<div class="text-column">
	<table>
		<thead>
			<tr>
				<th style="width: 30px;">ID</th>
				<th>Title</th>
				<th>Content</th>
				<th style="width: 100px;">Date</th>
			</tr>
		</thead>
		{#await my}
			<p>...Loading</p>
		{:then my}
			{#if my.length === 0}
				<p>...Loading</p>
			{:else}
				<tbody>
					{#each getPaginatedItems(currentPage) as item, index}
						<tr>
							<td style="text-align: center">{item.id}</td>
							<td><a href="/board/{item.id}" class="board-link">{item.title}</a></td>
							<td>{item.content}</td>
							<td>
								{new Date(item.create_date)
									.toISOString()
									.slice(0, 10)}
							</td>
						</tr>
					{/each}
				</tbody>
			{/if}
		{:catch error}
			<p>ajax 오류가 발생했습니다.</p>
		{/await}
	</table>
	{#if totalPages > 1}
		<div class="page-num">
			{#if currentPage>1}
			<a href="#" on:click={() => changePage(0)}>&laquo;</a>
			{/if}
			{#each getPages() as page}
				<span class:active={currentPage === page}>
					<a href="#" on:click={() => setPage(page)}>{page}</a>
				</span>
			{/each}
			{#if currentPage<totalPages}
			<a href="#" on:click={() => changePage(1)}>&raquo;</a>
			{/if}
		</div>
	{/if}
</div>