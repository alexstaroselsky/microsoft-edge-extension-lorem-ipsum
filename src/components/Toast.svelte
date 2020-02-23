<script>
  import { createEventDispatcher } from "svelte";

  export let message = "";

  const dispatch = createEventDispatcher();

  function handleClick() {
    dispatch("close");
  }
</script>

<style>
  .toast {
    max-width: 350px;
    overflow: hidden;
    font-size: 0.875rem;
    background-color: rgba(255, 255, 255, 0.85);
    background-clip: padding-box;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.15);
    -webkit-backdrop-filter: blur(10px);
    backdrop-filter: blur(10px);
    border-radius: 0.25rem;
    opacity: 1;
    display: block;
  }

  .toast:not(:last-child) {
    margin-bottom: 0.75rem;
  }

  .toast-header {
    display: flex;
    align-items: center;
    padding: 0.25rem 0.75rem;
    color: #6c757d;
    background-color: rgba(255, 255, 255, 0.85);
    background-clip: padding-box;
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
  }

  .toast-body {
    padding: 0.75rem;
  }

  .close {
    font-size: 1.5rem;
    font-weight: 700;
    line-height: 1;
    color: #000;
    text-shadow: 0 1px 0 #fff;
    opacity: 0.5;
  }

  .close:hover {
    color: #000;
    text-decoration: none;
  }

  .close:not(:disabled):not(.disabled):hover,
  .close:not(:disabled):not(.disabled):focus {
    opacity: 0.75;
  }

  button.close {
    padding: 0;
    background-color: transparent;
    border: 0;
    -webkit-appearance: none;
    -moz-appearance: none;
    appearance: none;
  }
</style>

<div
  aria-live="polite"
  aria-atomic="true"
  class="d-flex justify-content-center align-items-center"
  style="min-height: 200px;">

  <!-- Then put toasts within -->
  <div class="toast" role="alert" aria-live="assertive" aria-atomic="true">
    <div class="toast-header">
      <strong class="mr-auto">Lorem Ipsum</strong>
      <button
        type="button"
        class="ml-2 mb-1 close"
        data-dismiss="toast"
        aria-label="Close"
        on:click={handleClick}>
        <span aria-hidden="true">&times;</span>
      </button>
    </div>
    <div class="toast-body">{message}</div>
  </div>
</div>
