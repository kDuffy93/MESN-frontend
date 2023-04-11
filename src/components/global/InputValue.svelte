<script>
  export let inputId;
  export let inputName;

  export let inputPlaceholder;
  export let value = "";
  export let min;
  export let max;
  export let step;
</script>

<input bind:value id={inputId} name={inputName} placeholder={inputPlaceholder} size="15" {min} {max} {step} />

<style>
  #rangeBedrooms {
    width: 100%;
    margin: 10px;
  }
  #shortterm,
  #middleterm,
  #longterm,
  #spring,
  #summer,
  #fall,
  #winter {
    width: 20px;
    margin: 0;
  }
  #minprice,
  #maxprice {
    border: none;
    border-bottom: black solid 2px;
  }
</style>
