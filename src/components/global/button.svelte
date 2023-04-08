<!-- js -->
<script>
  // some of the buttons could have
  export let buttonId;
  // export let buttonText;
  export let buttonColorVar = "--default-button-color";
  //export let borderRadius = '--default-border-radius';
  export let buttonIconClass = "fa-solid fa-plus fa";
  export let classList = "btn btn_house";
</script>

<!-- every button have:    -->
<!-- html -->
<button on:click id={buttonId} class={classList} style="background-color:var({buttonColorVar});">
  {#if buttonIconClass}<i class={buttonIconClass} />{/if}
</button>

<!-- css -->
<style>
  .btn {
    overflow: hidden;
    position: relative;
    width: 60px;
    height: 60px;
    text-align: center;
    margin: 10px 10px;
    border-radius: 15px;
    box-shadow: 0 5px 15px -5px rgba(0, 0, 0, 0.1);
  }
  .fa {
    font-size: 27px;
    transform: scale(1);
    line-height: 50px;
    transition: all 0.4s cubic-bezier(0.31, -0.1, 0.43, 1.59);
  }
  .btn::before {
    content: "";
    position: absolute;
    top: 90%;
    left: -110%;
    width: 120%;
    height: 120%;
    transform: rotate(45deg);
    transition: all 0.4s cubic-bezier(0.31, -0.1, 0.43, 1.59);
  }
  .btn .dl1 {
    color: #ede682;
  }
  .btn_dl1::before {
    background-color: #ede682;
  }

  .btn .dl2 {
    color: #febf63;
  }
  .btn_dl2::before {
    background-color: #febf63;
  }

  .btn .fa-house-signal {
    color: #ade498;
  }
  .btn_house::before {
    background-color: #ade498;
  }

  .btn .fa-plus {
    color: #476cf1;
  }
  .btn_add::before {
    background-color: #476cf1;
  }

  .btn:hover::before {
    top: -10%;
    left: -10%;
  }
  .btn:hover .fa {
    color: #fff;
    transform: scale(1.3);
  }
  i {
    pointer-events: none;
  }
</style>
