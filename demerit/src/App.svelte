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

			<hr style="width:480px; margin-left:10px;">

			<BodyParts window={window}/>
		</div>
		<div id="live-preview">

			<div id="inner-body">

				<DemoView/>

			</div>

			<!--<DemoView/>-->

			<!--<DemoView/>-->
		</div>
	</div>
</main>

<style lang="scss">

	$height:100vh;

	@media only screen and (min-width:501px) {
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
				scrollbar-width:none;

				& p {
					margin-left:10px;
					margin-bottom:0px;
					font-size:20px;
				}
			}

			#live-preview {
				width:calc(100vw - 500px);
				height:$height;
				position:absolute;
				right:0px;
				top:0px;
				background-color:rgba(128, 128, 128, 0.4);
				overflow:scroll;
				-webkit-scrollbar:none;
				-moz-scrollbar:none;
				scrollbar-width:none;

				#inner-body {
					display:inline-block;
					padding:25px;
				}
			}
		}
	}

	@media only screen and (max-width:500px) {
		#main-area {
			width:100vw;
			height:$height;
			overflow:hidden;
			position:relative;

			#editor-area {
				width:100vw;
				height:100vh;
				position:absolute;
				top:0px;
				left:0px;
				z-index:1000000;
				background-color:#fff;
				overflow:scroll;

				& p {
					margin-left:10px;
					margin-bottom:0px;
					text-decoration:underline;
				}
			}
		}
	}
	
</style>