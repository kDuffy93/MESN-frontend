<!-- leave empty -->
<script>
    export let buttonId;
    export let buttonText = 'default text';
    export let buttonColor = 'red';
  </script>
  
  <!-- html -->
  <button id={buttonId} style='--buttoncolor:{buttonColor};'>
    {buttonText}
  </button>
  
  <!-- css -->
  <style>
    button {
      color: var(--buttoncolor);
    }
  </style>