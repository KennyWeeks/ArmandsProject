<script>

    export let buttonText = "click"
    export let printbutton = false;

</script>

<button class="clickbutton" class:printbutton={printbutton === true}>{buttonText}</button>

<style lang="scss">

    .clickbutton {
        padding:10px;
        border:2px solid #000;
        text-transform:uppercase;
        border-radius:5px;
        box-shadow:0px 0px 10px rgba(0,0,0,0.3);
    }

    .printbutton {
        background-color:#000;
        color:#fff;
    }

</style>