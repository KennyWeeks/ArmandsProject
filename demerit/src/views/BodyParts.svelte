<script>

    import {onMount} from "svelte";

    import Button from "../components/Button.svelte";
    import TextArea from "../components/TextArea.svelte";
    import Input from "../components/Input.svelte";
    var textArea;
    var time;
    var points;
    var assigner;
    var inputs;
    var desc;
    var name;
    var date;
    var hrNum;
    export let window;

    var printCommand = ()=>{
        let mainContent = document.getElementById("main-component");
        let CurrentArray = Array.from(mainContent.childNodes);
        CurrentArray = CurrentArray.filter((val)=>{return val.data != " "})

        //Create the new window
        let height = 8.5 * 96;
        let width = 11 * 96;
        let newWindow = window.open("", "PRINT", `height=${height}px, width=${width}px`);

        //Add the main-component to the new page
        newWindow.document.write("<div id='main-component'></div>");
        let newMainComponent = newWindow.document.getElementById("main-component");

        //Save the content to the new window
        newMainComponent.innerHTML = mainContent.innerHTML; 
        let newMainArray = Array.from(newMainComponent.childNodes);

        //Parse the array
        newMainArray = newMainArray.filter((val)=>{return val.data != " "})

        //Save the current styles to the new page
        newMainComponent.setAttribute("style", mainContent.getAttribute("style"));

        //Save the inner components styles from this page to the new page
        for(let i = 0; i < newMainArray.length; i++) {
            newMainArray[i].setAttribute("style", CurrentArray[i].getAttribute("style"));
        }

        newWindow.focus();
        
    }

    onMount(async ()=>{
        window = window;
        textArea = document.getElementsByTagName("textarea")[0];
        time = document.getElementById("time");
        points = document.getElementById("demerit-points");
        assigner = document.getElementById("assigned");
        desc = document.getElementById("demerit-description");
        name = document.getElementById("name-text");
        date = document.getElementById("date-text");
        hrNum = document.getElementById("number-text");
        //This tag works on the input
        inputs = document.getElementsByTagName("input");
        inputs = Array.from(inputs);
        let dateTime = new Date();
        console.log(dateTime.getHours());
        console.log(dateTime.getMinutes());
        let select = document.getElementsByTagName("select");
        select = Array.from(select);
        select.forEach((e)=>{
            console.log("Hello");
            if(e.getAttribute("name")=="hours") {
                e.value = dateTime.getHours();
            }

            if(e.getAttribute("name")=="minutes") {
                e.value = dateTime.getMinutes();
            }

            if(e.getAttribute("name")=="ampm") {
                if(dateTime.getHours() > 12) {
                    e.value = "pm";
                }
            }
        });
    });

</script>

<div class="bodypart">

    <Input labelTag="Name" def="Jon/Jane Doe"/><br>
    <Input labelTag="Date" type="date"/><br>
    <Input labelTag="HR-Number" def=111111111/><br>
    <hr>
    <Input labelTag="Demerit-points" type="number" def="0" min={0}/><br>
    <!--<Input labelTag="Time" type="time"/><br>-->
    <label for="hours" style="margin-bottom:10px;">Time of Demerit</label>
    <select name="hours" id="hours-tag">
        {#each Array.from(Array(24).keys(),n=>n+1) as n}
            <option value="{n}">{n}</option>
        {/each}
    </select>
    <select name="minutes" id="minutes">
        {#each Array.from(Array(60).keys(),n=>n+1) as n}
            <option value="{n}">{n}</option>
        {/each}
    </select>
    <select name="ampm" id="ampm-tag">
        <option value="am" default>AM</option>
        <option value="pm">PM</option>
    </select><br>
    <Input labelTag="Who-assigned-the-demerit" def="Captain ..."/><br>
    <hr>
    <TextArea/>
    <br>
    <Button printbutton={true} buttonText={"print"} on:click={()=>{
        //I want to run value checks here because we want to make sure
        //the data isn't default
        console.log(inputs[0].value);

        inputs.forEach((e)=>{
            console.log(e.getAttribute("type"));
            if(["text", "number"].indexOf(e.getAttribute("type")) >= 0 && e.value.length == 0) {
                e.style.outlineStyle = "solid";
                e.style.outlineColor = "#ff0000";
            }
        });
        
        if(textArea.value.length == 0) {
            textArea.style.outlineStyle = "solid";
            textArea.style.outlineColor = "#ff0000";
        }

        /*name.innerText = inputs[0].value;
        date.innerText = inputs[1].value;
        hrNum.innerText = inputs[2].value;
        points.innerText = inputs[3].value;
        time.innerText = inputs[4].value;
        assigner.innerText = inputs[5].value;
        desc.innerText = textArea.value;*/
        //printCommand();
    }}/>
</div>

<style lang="scss">

    .bodypart {
        padding:10px;
        width:480px;
        position:absolute;
    }
    @media only screen and (max-width:500px) {
        .bodypart {
            width:calc(100vw - 20px);
        }
    }

</style>