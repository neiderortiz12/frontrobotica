<script>
	//export let name;
	import Scara from './components/Scara.svelte'
	import Puma from './components/Puma.svelte'
	import Cilindrico from './components/Cilindrico.svelte'
	let currentPage = Scara;

	function chagePage(newPage){
		currentPage=newPage
	}
</script>

<main>
	<header>
		<img src="./assets/banner.jpg" alt="">
	</header>
	<div class="nav">
		<button on:click={() => chagePage(Scara)}>Scara</button>
		<button on:click={() => chagePage(Puma)}>Puma</button>
		<button on:click={() => chagePage(Cilindrico)}>Cilíndrico</button>
	</div>
	<div>
		<svelte:component this={currentPage}/>
	</div>
	
</main>

<style>
	header{
		width: 100%;
		height: 8rem;
		background-color: goldenrod;
		font-size: 5rem;
	}
	.nav{
		display: grid;
		grid-gap: 5px;
		grid-template-columns: repeat(3,1fr);
		justify-content: center;
	}
	button{
        background-color:rgb(34, 34, 63);
        color: cornsilk;
    }
	button:hover{
		background-color: rgb(112, 136, 112);
		color: azure;
	}
	img{
		width: 100%;
		height: auto;
	}

</style>