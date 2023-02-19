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
        
    });

</script>

<div class="bodypart">

    <Input labelTag="Name"/><br>
    <Input labelTag="Date" type="date"/><br>
    <Input labelTag="HR-Number"/><br>
    <hr>
    <Input labelTag="Demerit-points" type="number" def="0" min={0}/><br>
    <Input labelTag="Time" type="time"/><br>
    <Input labelTag="Who-assigned-the-demerit" def="Captain ..."/><br>
    <hr>
    <TextArea/>
    <br>
    <Button printbutton={true} buttonText={"print"} on:click={()=>{
        name.innerText = inputs[0].value;
        date.innerText = inputs[1].value;
        hrNum.innerText = inputs[2].value;
        points.innerText = inputs[3].value;
        time.innerText = inputs[4].value;
        assigner.innerText = inputs[5].value;
        desc.innerText = textArea.value;
        //printCommand();
    }}/>
</div>

<style lang="scss">

    .bodypart {
        padding:10px;
        width:480px;
        position:absolute;
    }

</style>