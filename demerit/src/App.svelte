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

			#close-tab {
				width:100px;
				height:50px;
				border-radius:15px;
				position:fixed;
				top:10px;
				right:-50px;
				box-shadow:0 0 5px rgba(0,0,0,0.3);
				background-color:#fff;
				z-index:1000000000;
				transition:right .5s linear;
			}

			#editor-area {
				width:100vw;
				height:100vh;
				position:absolute;
				top:0px;
				left:0px;
				z-index:1000000;
				background-color:#fff;
				overflow:scroll;
				scrollbar-width:none;
				transition:left .5s linear;

				& p {
					margin-left:10px;
					margin-bottom:0px;
					font-size:20px;
				}
			}
		}
	}
	
</style>