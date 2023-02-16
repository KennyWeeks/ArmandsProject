<script>

    import {onMount} from "svelte";

    import Button from "../components/Button.svelte";
    import TextArea from "../components/TextArea.svelte";
    import Input from "../components/Input.svelte";
    var textArea;

    onMount(async ()=>{
        textArea = document.getElementsByTagName("textarea")[0];
    });

</script>

<div class="bodypart">

    <Input labelTag="Demerit-points"/><br>
    <Input labelTag="Time"/><br>
    <Input labelTag="Infaction"/><br>
    <Input labelTag="Who-assigned-the-demerit"/><br>
    <TextArea/>
    <br>
    <Button printbutton={true} buttonText={"print"} on:click={()=>{
        console.log(textArea.value)
        alert("Hello")
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