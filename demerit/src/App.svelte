<script>
	import BodyParts from "./views/BodyParts.svelte";
	import DemoView from "./views/DemoView.svelte";
	import {onMount} from "svelte";
	let wind = null;
	let toggle = 0;

	onMount(async ()=>{
		wind = window;
		/*window.addEventListener("resize", ()=>{
			let ea = document.getElementById("editor-area");
			let ct = document.getElementById("close-tab");
			ea.removeAttribute("style");
			ct.removeAttribute("style");
		});*/
	});

	const resizeCheck = (element, parent)=>{
		let minW = (8.5 * 96 * 0.5);
		let maxW = 8.5 * 96;

		if(parent.offsetWidth <= maxW && parent.offsetWidth >= minW) {
			let scale = 1 - 1 * (1 - parent.offsetWidth / (8.5 * 96));
			element.style.transform = `scale(${scale})`;
		} else {
			element.style.transform = "scale(1.0)";
		}
	}

</script>

<svelte:window on:resize="{()=>{
	let mc = document.getElementById("main-component");
	let livePreview = document.getElementById("live-preview");
	resizeCheck(mc, livePreview);
}}"/>

<!--<svelte:window on:resize="{()=>{
	let test = document.getElementById("main-component");
	let livePreview = document.getElementById("live-preview");
	let w = (8.5 * 96) * 0.5;

	if(livePreview.offsetWidth <= 8.5 * 96 && livePreview.offsetWidth >= w) {
		let sc = 1 - 1 * (1 - livePreview.offsetWidth / (8.5 * 96));
		test.style.transform = "scale(" + sc + ")";
	} else if(livePreview.offsetWidth > 8.5 * 96) {
		test.style.transfrom = "scale(1.0)"; 
	}
}}" on:load="{()=>{
	let test = document.getElementById("main-component");
	let livePreview = document.getElementById("live-preview");
	let w = (8.5 * 96) * 0.5;
	if(livePreview.offsetWidth <= 8.5 * 96 && livePreview.offsetWidth >= w) {
		let sc = 1 - 1 * (1 - livePreview.offsetWidth / (8.5 * 96));
		test.style.transform = "scale(" + sc + ")";
	}
}}"/>-->

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
			
		}} on:keydown|preventDefault="{()=>{}}">
		
			<div class="images">

				<img src="eye.png" width="35px" alt="preview tab"/>

			</div>

			<div class="images">

				<img src="generate.png" width="25px" alt="generate text"/>

			</div>
	
		</div>
	
		<div id="editor-area">

			<p>Write your data here</p>

			<hr style="margin-left:10px;">

			<BodyParts window={window}/>
		</div>

		<div id="live-preview">

			<!--I will make this toggle it's own component-->

			<div id="inner-body">

				<DemoView/>

			</div>

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

			hr {
				width:480px;
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

	@media only screen and (min-width:calc(501px + 8.5 * 96px * 0.5)) {
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

	@media only screen and (max-width:calc(500px + 8.5 * 96px)) and (min-width:calc(501px + 8.5 * 96px * 0.5)) {
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
			overflow:hidden;

			.images {
				width:50px;
				height:50px;
				box-shadow:inset 0 0 0 1px #000;
			}
		}

		/*#inner-body {
			filter:blur(8px);
		}*/
	}

	@media only screen and (max-width:calc(500px + 8.5 * 96px * 0.5)) {
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
				overflow:hidden;
				display:flex;
				justify-content:space-between;
				flex-flow:row;
				flex-wrap:nowrap;

				.images {
					width:50px;
					height:50px;
					margin:0px;
					position:relative;

					img {
						position:absolute;
						top:50%;
						left:50%;
						transform:translate(-50%, -50%);
					}
				}
			}

			#editor-area {
				width:$width;
				height:$height;
				transition:left .5s linear;

				hr {
					width:calc(100vw - 20px);
				}
			}

			#live-preview {
				width:$width;
				height:$height;
			}
		}
	}
	
</style>