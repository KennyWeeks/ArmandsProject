<script></script>

<div id="main-component">

    <img src="header.png"/>

    <div id="header">

        <div class="itemblocks" id="test">

            <h3 class="description">Name</h3>

        </div>

        <div class="itemblocks">

            <h3 class="description">Date</h3>

        </div>

        <div class="itemblocks">

            <h3 class="description">HR #</h3>

        </div>

    </div>

    <h3 id="infraction">Infraction:</h3>

</div>

<style lang="scss">

    #main-component {
        /*This is gonna be the piece of paper*/
        width:calc(8.5*96px);
        height:calc(11*96px);
        box-shadow:0 0 0 1px #000;
        position:absolute;
        top:100vh;
        left:50%;
        transform:translate(-50%);
        margin-bottom:10px;
        overflow:hidden;

        img {
            margin-top:calc(1*96px);
            margin-left:calc(1*96px);
            border:2px solid #000;
        }

        #header {
            width:calc(6.5*96px);
            border-bottom:3px solid #000;
            display:flex;
            justify-content:space-between;
            flex-flow:row;
            flex-wrap:nowrap;
            margin-left:96px;

            #test {
                flex-grow:2;
            }

            .itemblocks {
                flex-grow:1;
            }

            .itemblocks > h3 {
                font-size:18px;
                margin-bottom:0px;
            }
        }

        #infraction {
            text-transform:uppercase;
            font-weight:normal;
            margin-left:96px;
            font-size:16px;
        }
    }

</style>