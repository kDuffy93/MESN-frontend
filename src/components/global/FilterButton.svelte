<script>
  export let buttonId;
  export let buttonClass = "btn btn-primary";
  export let buttonIconClass;
  export let buttonText;
  export let buttonType = "button";
</script>

<button on:click id={buttonId} class={buttonClass} type={buttonType}>
  {#if buttonIconClass}<i class={buttonIconClass} />{/if}
  {buttonText}
</button>

<style>
  #filterButton {
    position: relative;
    width: 100px;
    height: 60px;
    text-align: center;
    font-size: 17px;
    /* margin: 10px 10px; */
    border-radius: 15px;
    box-shadow: 0 5px 15px -5px rgb(0 0 0 / 10%);
  }
  .cityTownButton,
  .housingTypeButton {
    position: relative;
    width: auto;
    height: 50px;
    font-size: 17px;
    text-align: center;
    margin: 10px 10px;
    padding: 0 12px;
    border-radius: 10px;
    box-shadow: 0 5px 15px -5px rgb(0 0 0 / 10%);
  }
</style>
