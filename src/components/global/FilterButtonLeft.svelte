<script>
    export let buttonId;
    export let buttonClass = "btn btn-primary";
    export let buttonIconClass;

    export let buttonType = "button";
    export let buttonTitle;
  </script>
  
  <button on:click id={buttonId} class={buttonClass} title={buttonTitle} type={buttonType}>
    {#if buttonIconClass}<i class={buttonIconClass} />{/if}
  
  </button>
  
  <style>
    #filterButton {
      position: relative;
      /* width: 100px; */
      width: 60px;
      height: 60px;
      text-align: center;
      font-size:27px;
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
      box-shadow: 0 5px 15px -5px rgb(0 0 0 / 10%);  background-color: #f9f9f9;
    
  
    }
  
  .active{
  
  background-color: #999999;
  
  }
  
  
  </style>
  