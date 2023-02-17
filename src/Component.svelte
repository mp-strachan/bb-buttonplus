<script>
  import { getContext } from "svelte"

  export let customContents
  export let text

  export let variant
  export let size
  export let quiet
  export let disabled

  export let btnClicked

  export let bgColour
  export let bgHover
  export let txtColour
  export let txtHover
  export let brdColour
  export let brdHover

  const { styleable } = getContext("sdk")
  const component = getContext("component")

  $: disabled = disabled ? "disabled" : ""

</script>

<div use:styleable={$component.styles}>
  <button on:click={btnClicked} class="
            spectrum-Button spectrum-Button--size{size}
            spectrum-Button--{variant}
            {quiet === true ? ' spectrum-Button--quiet' : ''}
          " {disabled}
          style="
            --bgColour:{bgColour}; --bgHover:{bgHover};
            --txtColour:{txtColour}; --txtHover:{txtHover};
            --brdColour:{brdColour}; --brdHover:{brdHover};
          ">
    {#if customContents}
      <slot />
    {:else}
      {text}
    {/if}
  </button>
</div>

<style>
  .spectrum-Button--custom {
    background-color: var(--bgColour, black);
    color: var(--txtColour, white);
    border-color: var(--brdColour, white);
  }

  .spectrum-Button--custom:hover {
    background-color: var(--bgHover, black);
    color: var(--txtHover, white);
    border-color: var(--brdHover, white);
  }
</style>
