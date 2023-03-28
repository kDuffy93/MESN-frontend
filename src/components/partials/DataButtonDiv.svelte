<script>
  function handleClick1() {
    alert('Button1 clicked!');
  }
  function handleClick2() {
    alert('Button2 clicked!');
  }
  function handleClick3() {
    alert('Button3 clicked!');
  }
  function handleClick4() {
    alert('Button4 clicked!');
  }
</script>

<div class="dataButtonDiv">
  <a href="#" on:click={handleClick1} class="btn btn_house"
    ><i class="fa-solid fa-house-signal fa" /></a
  >
  <a href="#" on:click={handleClick2} class="btn btn_add"
    ><i class="fa-solid fa-plus fa" /></a
  >
  <a href="#" on:click={handleClick3} class="btn btn_dl1"
    ><i class="fa-solid fa-arrow-down-wide-short dl1 fa" /></a
  >

  <a href="#" on:click={handleClick4} class="btn btn_dl2"
    ><i class="fa-solid fa-arrow-down-a-z dl2 fa" /></a
  >
</div>

<style>
  .dataButtonDiv .btn {
    overflow: hidden;
    position: relative;
    width: 60px;
    height: 60px;
    text-align: center;
    margin: 10px 10px;
    border-radius: 15px;
    background-color: #fff;
    box-shadow: 0 5px 15px -5px rgba(0, 0, 0, 0.1);
  }
  .dataButtonDiv .fa {
    font-size: 27px;
    transform: scale(1);
    line-height: 50px;
    transition: all 0.4s cubic-bezier(0.31, -0.1, 0.43, 1.59);
  }
  .dataButtonDiv .btn::before {
    content: '';
    position: absolute;
    top: 90%;
    left: -110%;
    width: 120%;
    height: 120%;
    transform: rotate(45deg);
    transition: all 0.4s cubic-bezier(0.31, -0.1, 0.43, 1.59);
  }
  .dataButtonDiv .btn .dl1 {
    color: #ede682;
  }
  .dataButtonDiv .btn_dl1::before {
    background-color: #ede682;
  }

  .dataButtonDiv .btn .dl2 {
    color: #febf63;
  }
  .dataButtonDiv .btn_dl2::before {
    background-color: #febf63;
  }

  .dataButtonDiv .btn .fa-house-signal {
    color: #ade498;
  }
  .dataButtonDiv .btn_house::before {
    background-color: #ade498;
  }

  .dataButtonDiv .btn .fa-plus {
    color: #476cf1;
  }
  .dataButtonDiv .btn_add::before {
    background-color: #476cf1;
  }

  .dataButtonDiv .btn:hover::before {
    top: -10%;
    left: -10%;
  }
  .dataButtonDiv .btn:hover .fa {
    color: #fff;
    transform: scale(1.3);
  }
</style>
