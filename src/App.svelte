<script>
  import { fly } from "svelte/transition";
  import { quintOut } from "svelte/easing";
  import { loremIpsum } from "lorem-ipsum";
  import IconCopy from "./components/IconCopy.svelte";
  import Toast from "./components/Toast.svelte";

  let count = 3;
  let units = "sentences";
  let showToast = false;

  $: output = loremIpsum({
    count,
    units
  });

  function handleCopyClick() {
    navigator.clipboard.writeText(output).then(() => {
      showToast = true;

      setTimeout(() => {
        showToast = false;
      }, 3000);
    });
  }
</script>

<style>
  h1 {
    color: #0d6efd;
    text-transform: uppercase;
    font-size: 1.25rem;
    font-weight: 100;
  }
</style>

<div class="container-fluid">
  <Toast message="Text copied to clipboard!" show={showToast} />

  <main class="mb-3">
    <h1 class="mt-3">Lorem Ipsum Generator</h1>

    <form>
      <div class="form-row">
        <div class="form-group mb-2 col">
          <label for="count">Count:</label>
          <input
            type="number"
            id="count"
            name="count"
            class="form-control"
            bind:value={count}
            min="1"
            max="99"
            required />
        </div>
      </div>

      <div class="form-row">
        <div class="form-group mb-2 col">
          <label for="units">Units:</label>
          <select
            name="units"
            id="units"
            class="form-control form-select"
            bind:value={units}
            required>
            <option value="words">Word(s)</option>
            <option value="sentences">Sentence(s)</option>
            <option value="paragraphs">Paragraph(s)</option>
          </select>
        </div>
      </div>

      <div class="form-row">
        <div class="col">
          <label for="output">Output:</label>
          <div class="input-group mb-2">
            <textarea
              class="form-control"
              id="output"
              name="output"
              rows="5"
              bind:value={output}
              aria-label="With textarea" />
            <div class="input-group-append">
              <button
                class="btn btn-primary"
                type="button"
                id="copy"
                on:click={handleCopyClick}>
                <IconCopy />
              </button>
            </div>
          </div>
        </div>
      </div>
    </form>
  </main>
</div>
