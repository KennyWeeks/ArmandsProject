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
</script>

<svelte:window on:resize="{()=>{
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
}}"/>

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

			<!--I will make this toggle it's own component-->

			<p id="zoomed-in">scale: <span id="amount">1</span></p>

			<div id="zoom-in-toggle">

				<div id="boundary-overlay" on:mousedown|preventDefault="{(e)=>{
					let zoomIn = document.getElementById("zoom-in-toggle");
					var toggle = document.getElementById("toggle");
					var elementX = zoomIn.offsetLeft;
					var xPos = e.target.offsetLeft;
					var xW = e.target.offsetWidth;
					e.target.addEventListener("mousemove", (ev)=>{
						if(elementX + xPos + 10 <= ev.clientX && ev.clientX <= elementX + xPos + xW - 10) {
							let diff = ev.clientX - (elementX + xPos + 10);
							toggle.style.left = diff + "px";
						} else if(ev.clientX < elementX + xPos + 10) {
							toggle.style.left = "0px";
						} else {
							toggle.style.left = "170px";
						}
					});
				}}"></div>

				<div id="boundary">

					<div id="toggle"></div>

					<div id="line"></div>

				</div>

			</div>

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

			#zoomed-in {
				font-weight:bold;
				font-size:15px;
				position:fixed;
				z-index:100000000000;
				top:0px;
				right:225px;
				margin-top:6px;
			}

			#zoom-in-toggle {
				width:200px;
				height:30px;
				background-color:#fff;
				position:fixed;
				top:0px;
				right:10px;
				z-index:100000;
				box-shadow:0 0 5px rgba(0,0,0,0.3);
				overflow:hidden;

				#boundary-overlay {
					width:190px;
					height:20px;
					position:absolute;
					z-index:1000;
					top:5px;
					left:5px;
				}

				#boundary {
					position:relative;
					height:20px;
					width:190px;
					margin-top:5px;
					margin-left:5px;

					#toggle {
						width:20px;
						height:20px;
						border-radius:50%;
						background-color:#000;
						position:absolute;
						top:0px;
						left:0px;
					}

					#line {
						width:190px;
						height:2px;
						background-color:#000;
						position:absolute;
						top:10px;
						left:0px;
						transform:translateY(-1px);
					}
				}
			}

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
				background-color:#00ff00;
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
		}

		/*#inner-body {
			filter:blur(8px);
		}*/
	}

	@media only screen and (max-width:calc(500px + 8.5 * 96px * 0.5)) {
		#main-area {
			overflow:hidden;
			background-color:#00ff00;

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