<!-- Input.svelte -->
<script>
    
    export let inputId;
    export let inputName;
   
    export let summerChecked;
export let fallChecked;

  </script>
  

 
<input type="checkbox" bind:checked={summerChecked} id={inputId} name={inputName}/>
    Summer
 
  

    <input type="checkbox" bind:checked={fallChecked} id={inputId} name={inputName} />
    Fall

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