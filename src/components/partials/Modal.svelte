<script>
  let shown = false;

  export function show() {
    shown = true;
  }

  export function hide() {
    shown = false;
  }
</script>

{#if shown}
  <div class="modal-wrapper" />
  <div class="modal" />
  <span>&times;</span>
  <slot />
{/if}

<style>
  .modal-wrapper {
    background-color: rgb(0, 0, 0);
    background-color: rgba(0, 0, 0, 0.6);
    position: fixed;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    z-index: 1;
  }

  .modal {
    background-color: white;
    max-width: 70vw;
    padding: 1rem;
    margin: 15% auto;
    max-height: 80vh;
    z-index: 999;
  }

  .close-button {
    position: absolute;
    top: 0;
    right: 0;
  }
</style>
