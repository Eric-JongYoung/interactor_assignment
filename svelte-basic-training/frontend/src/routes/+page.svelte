<script>

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="main">
		<img src="/src/lib/images/basic_logo.png" alt="SvelteKit" class="s-Cmt25qOMERl7">
		<div class="main-content">
		고종영<br>
		1번째 과제 내용 입니다.<br>
		감사합니다.
		</div>
	</div>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
	.main{
		text-align: center;
	}
	.main-content{
		font-family: 'LINESeedKR-Bd';
	}
</style>
