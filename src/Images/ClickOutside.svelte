<script>
  // from https://github.com/joeattardi/svelte-click-outside
  import { createEventDispatcher } from "svelte";
  export let exclude = [];
  export let className;
  let child;
  const dispatch = createEventDispatcher();
  function isExcluded(target) {
    var parent = target;
    while (parent) {
      if (exclude.indexOf(parent) >= 0 || parent === child) {
        return true;
      }
      parent = parent.parentNode;
    }
    return false;
  }
  function onClickOutside(event) {
    if (!isExcluded(event.target)) {
      event.preventDefault();
      dispatch("clickoutside");
    }
  }
</script>

<svelte:body on:click={onClickOutside} />
<div bind:this={child} class={className}>
  <slot />
</div>
