<script></script>

<label for="textarea">Type demerit details here</label>
<textarea name="textarea" rows="20" placeholder="Write demerit details here ..." on:focus="{(e)=>{
    e.target.style.outlineStyle = "none";
}}"></textarea>

<style lang="scss">

    label {
        margin-bottom:10px;
    }

    textarea[name="textarea"] {
        border-radius:5px;
        resize:none;
        width:480px;
    }

    textarea[name="textarea"]:focus {
        outline:none;
    }

    @media only screen and (max-width:500px) {
        textarea[name="textarea"] {
            width:calc(100vw - 20px);
        }
    }

</style>