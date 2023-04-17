<script>
  import Button from "../global/button.svelte";
</script>

<div class="dataButtonDiv">
  <Button on:click buttonId={"home"} classList="btn btn_house" buttonIconClass="fa-solid fa-house-signal fa" buttonTitle={"Get Data"}/>
  <Button on:click buttonId={"add"} classList="btn btn_add" buttonIconClass="fa-solid fa-plus fa" buttonTitle="Add Data"/>
  <Button on:click buttonId={"current"} classList="btn btn_dl1" buttonIconClass="fa-solid fa-arrow-down-wide-short dl1 fa" buttonTitle="Download Current"/>
  <Button on:click buttonId={"all"} classList="btn btn_az" buttonIconClass="fa-solid fa-arrow-down-a-z dl2 fa" buttonTitle="Download All"/>
</div>

<style>
</style>
