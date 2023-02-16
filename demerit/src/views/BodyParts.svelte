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

    onMount(async ()=>{
        textArea = document.getElementsByTagName("textarea")[0];
        time = document.getElementById("time");
        points = document.getElementById("demerit-points");
        inputs = document.getElementsByTagName("input");
        assigner = document.getElementById("assigned");
    });

</script>

<div class="bodypart">

    <Input labelTag="Demerit-points" type="number"/><br>
    <Input labelTag="Time" type="time"/><br>
    <Input labelTag="Infaction"/><br>
    <Input labelTag="Who-assigned-the-demerit"/><br>
    <TextArea/>
    <br>
    <Button printbutton={true} buttonText={"print"} on:click={()=>{
        console.log(textArea.value)
        points.innerText = inputs[0].value;
        time.innerText = inputs[1].value;
        assigner.innerText = inputs[3].value;
    }}/>
</div>

<style lang="scss">

    .bodypart {
        padding:10px;
        border:2px solid #000;
        position:absolute;
        top:50%;
        left:50%;
        transform:translate(-50%, -50%);
    }

</style>