<script>
	import BodyParts from "./views/BodyParts.svelte";
	import DemoView from "./views/DemoView.svelte";
	import {onMount} from "svelte";
	let wind = null;

	onMount(async ()=>{
		wind = window;
	});
</script>

<main>
	<BodyParts window={window}/>
	<DemoView/>
	<div id="test"></div>
</main>

<style>

	#test {
		height:50px;
		width:100px;
		position:absolute;
		top:calc(100vh + (11*96px));
	}
</style>