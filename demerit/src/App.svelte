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
	<div id="main-area">
		<div id="editor-area">

			<p>Write your data here</p>

			<BodyParts window={window}/>
		</div>
		<div id="live-preview">
			<!--<DemoView/>-->
		</div>
	</div>
</main>

<style lang="scss">

	$height:100vh;

	#main-area {
		width:100vw;
		height:$height;
		position:relative;

		#editor-area {
			width:500px;
			height:$height;
			position:absolute;
			left:0px;
			top:0px;
			overflow:scroll;
		}

		#live-preview {
			width:calc(100vw - 500px);
			height:$height;
			position:absolute;
			right:0px;
			top:0px;
			background-color:rgba(128, 128, 128, 0.4);
		}
	}
	
</style>