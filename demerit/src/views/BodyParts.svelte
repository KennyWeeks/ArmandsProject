<script>

    import Button from "../components/Button.svelte";

</script>

<div class="bodypart">
    <Button printbutton={true} buttonText={"print"}/>
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