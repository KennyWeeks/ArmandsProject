<script>

    export let labelTag = "";
    export let type="text";
    export let def = "";

</script>

<label for="{labelTag}">{labelTag}</label><br>
<input type="{type}" name="{labelTag}" class="inputtag" required/>


<style lang="scss">

    label {
        display:inline-block;
    }

    input {
        outline:none;
    }

</style>