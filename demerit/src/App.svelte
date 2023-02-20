<script>
	import BodyParts from "./views/BodyParts.svelte";
	import DemoView from "./views/DemoView.svelte";
	import {onMount} from "svelte";
	let wind = null;
	let toggle = 0;

	onMount(async ()=>{
		wind = window;
		window.addEventListener("resize", ()=>{
			let ea = document.getElementById("editor-area");
			let ct = document.getElementById("close-tab");
			ea.removeAttribute("style");
			ct.removeAttribute("style");
		});
	});
</script>

<main>
	<div id="main-area">

		<div id="close-tab" on:click={(e)=>{
			let ea = document.getElementById("editor-area");
			let ct = document.getElementById("close-tab");
			if(toggle == 0) {
				ea.style.left = "-100vw";
				ct.style.right = "calc(100vw - 50px)";
				toggle+=1;
			} else {
				ea.style.left = "0vw";
				ct.style.right = "-50px";
				toggle-=1;
			}
			
		}}></div>
	
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

	$width:100vw;
	$height:100vh;

	#main-area {
		width:100vw;
		height:$height;
		position:relative;

		#editor-area {
			position:absolute;
			left:0px;
			top:0px;
			overflow:scroll;
			-webkit-scrollbar:none;
			-moz-scrollbar:none;
			scrollbar-width:none;
			background-color:#fff;
			z-index:1000000;

			& p {
				margin-left:10px;
				margin-bottom:0px;
				font-size:20px;
			}
		}

		#live-preview {		
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

	@media only screen and (min-width:501px) {
		#main-area {

			#editor-area {
				width:500px;
				height:$height;
			}

			#live-preview {
				width:calc(100vw - 500px);
				height:$height;
			}
			
		}
	}

	@media only screen and (max-width:calc(500px + 8.5*96px)) and (min-width:501px) {
		#close-tab {
			width:50px;
			height:50px;
			border-top-right-radius:15px;
			border-bottom-right-radius:15px;
			position:fixed;
			top:10px;
			left:500px;
			box-shadow:0 0 5px rgba(0,0,0,0.3);
			background-color:#fff;
			z-index:100000;
			transition:right .5s linear;
		}

		#inner-body {
			filter:blur(8px);
		}
	}

	@media only screen and (max-width:500px) {
		#main-area {
			overflow:hidden;

			#close-tab {
				width:100px;
				height:50px;
				border-radius:15px;
				position:fixed;
				top:10px;
				right:-50px;
				box-shadow:0 0 5px rgba(0,0,0,0.3);
				background-color:#fff;
				z-index:10000000000000;
				transition:right .5s linear;
			}

			#editor-area {
				width:$width;
				height:$height;
				transition:left .5s linear;
			}

			#live-preview {
				width:$width;
				height:$height;
			}
		}
	}
	
</style>