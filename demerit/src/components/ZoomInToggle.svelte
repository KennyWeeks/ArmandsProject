<script></script>

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


<style lang="scss">
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
</style>