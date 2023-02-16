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

    <p id="infraction-starting-line">I earned <span id="demerit-points">(#)</span> demerit points at approximately <span id="time">(time)</span> for a/an <span id="infraction-space">(infraction)</span>. <span id="assigned">(Who assigned
    you the demerits, if Capt. Spell out Captain)</span> assigned me this demerit report because <span id="demerit-description">...</span></p>

    <table cellspacing="0">
        <colgroup>
            <col span="1" style="width: 0%;">
            <col span="1" style="width: 45%;">
            <col span="1" style="width: 30%;">
            <col span="1" style="width: 25%;">
        </colgroup>
        <tr>
            <td></td>
            <td>Recruit Signature</td>
            <td>HR #</td>
            <td>Date</td>
        </tr>
        <tr>
            <td></td>
            <td>Academy Staff Signature</td>
            <td>HR #</td>
            <td>Date</td>
        </tr>
    </table>

</div>

<style lang="scss">

    #main-component {
        /*This is gonna be the piece of paper*/
        width:calc(8.5*96px);
        height:calc(11*96px);
        box-shadow:inset 0 0 0 1px #000;
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

        #infraction-starting-line {
            width:calc(6.5*96px);
            margin-left:96px;
            font-size:15.25px;
        }

        table {
            width:calc(6.5*96px + 2px);
            border-bottom:0.25px solid #000;
            border-right:0.25px solid #000;
            position:absolute;
            bottom:96px;
            left:96px;

            tr > td {
                box-shadow:inset 0 0 0 0.25px #000;
                overflow:hidden;
                padding:10px;
                padding-top:5px;
                padding-bottom:35px;
                font-style:italic;
                font-size:14px;
            }
        }
    }

</style>