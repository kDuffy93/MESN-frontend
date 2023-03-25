<!-- js -->
<script>
  // some of the buttons could have
  export let buttonId;
  export let buttonText = 'default text';
  export let buttonColorVar = '--default-button-color';
  export let borderRadius = '--default-border-radius';
</script>

<!-- every button have: -->
<!-- html -->
<button
  id={buttonId}
  style="background-color:var({buttonColorVar}); border-radius:var({borderRadius});"
>
  {buttonText}
</button>

<!-- css -->
<style>
</style>
