<script>
  export let heatId;
  export let heatClass;
  export let heatSpanClassOne;
  export let heatSpanClassTwo;
export let checked = false;

</script>

<!-- html -->
<label id={heatId} class={heatClass}>
  <input bind:checked={checked} type='checkbox' />
  <div>
    <span class={heatSpanClassOne} />
    <span class={heatSpanClassTwo} />
  </div>
  <i />
</label>

<!-- style -->
<style>
  label {
    transform: scale(0.6);
    display: block;
    width: 160px;
    background: #ccc;
    height: 80px;
    border-radius: 40px;
    background: linear-gradient(to bottom, #9e9e9e 30%, #f4f4f4);
    box-shadow: 0 2px 0 0 #fff, 0 -2px 0 0 #969494;
    position: relative;
    -webkit-tap-highlight-color: rgba(255, 255, 255, 0);
  }
  label input {
    display: none;
  }
  label div {
    display: block;
    width: 120px;
    height: 50px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    background: linear-gradient(to bottom, #8b8c8e 20%, #f4f4f4);
    border-radius: 25px;
  }
  label div:after {
    content: "";
    position: absolute;
    display: block;
    height: 46px;
    width: 116px;
    left: 2px;
    top: 2px;
    border-radius: 23px;
    background: #c5e0ee;
    box-shadow: inset 0 0 30px 0 rgba(0, 0, 0, 0.3);
    transition: 0.2s;
  }

  label i {
    display: block;
    width: 60px;
    height: 60px;
    position: absolute;
    background: linear-gradient(to top, #9e9e9e 20%, #f4f4f4);
    /* background-color: #FEBF63; */
    border-radius: 50%;
    box-shadow: 0 5px 10px 0 rgba(0, 0, 0, 0.7);
    top: 10px;
    left: 15px;
    transition: 0.25s;
  }
  label i:after {
    content: "";
    position: absolute;
    display: block;
    width: 52px;
    height: 52px;
    left: 4px;
    top: 4px;
    border-radius: 50%;
    background: #d5d4d4;
    /* background-color: #FEBF63; */
    z-index: 1;
  }

  label input:checked ~ i {
    top: 10px;
    left: 86px;
  }
  label input:checked + div:after {
    background: #ade498;
    box-shadow: inset 0 0 30px 0 rgba(0, 0, 0, 0.3);
  }
  label input:checked + div > .off {
    color: transparent;
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0);
  }
  label input:checked + div > .on {
    /* color: #C5E0EE; */
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0.3);
  }
  label:after {
    content: "";
    position: absolute;
    display: block;
    width: 164px;
    height: 84px;
    border-radius: 42px;
    /* background: red; */
    /* background-color: #C5E0EE; */
    top: -2px;
    left: -2px;
    z-index: -1;
    background: linear-gradient(to bottom, #969494, #fff);
  }
  label:hover {
    cursor: pointer;
  }
  label:focus,
  label:active {
    outline: 0;
  }
  .on,
  .off {
    text-transform: uppercase;
    position: absolute;
    left: 17px;
    top: 50%;
    transform: translateY(-50%);
    font-size: 1.2em;
    font-weight: 600;
    z-index: 2;
    -webkit-user-select: none;
    -moz-user-select: none;
    -ms-user-select: none;
    letter-spacing: 1px;
    transition: 0.25s;
  }
  .on {
    color: transparent;
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0);
  }
  .off {
    left: initial;
    right: 17px;
    color: #444;
    text-shadow: 0 1px 0 rgba(255, 255, 255, 0.2);
  }
</style>
