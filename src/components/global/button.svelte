<!-- js -->
<script>
  // some of the buttons could have
  export let buttonId;
  export let buttonText = 'default text';
  export let buttonColorVar = '--default-button-color';
  export let borderRadius = 15;
</script>

<!-- every button have: -->
<!-- html -->
<button
  on:click
  id={buttonId}
  style="background-color:var({buttonColorVar}); border-radius:var({borderRadius});"
>
  {buttonText}
</button>

<!-- css -->
<style>
</style>
