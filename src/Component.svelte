<script>
  import { getContext } from "svelte"
  import Countup from "svelte-countup"

  export let initial = '1'
  export let value = '10'
  export let duration = 1000
  export let step = 1
  export let roundto = 1
  export let format = false
  export let size

  const { styleable } = getContext("sdk")
  const component = getContext("component")

  $: sizeClass = `spectrum-Heading--size${size || "M"}`
  $: key = { initial, value, duration, step, roundto, format }
  $: {
    if (parseInt(value) < parseInt(initial)) {
      value = initial
    }
    if (!value) {
      value = 10
    }
    if (!initial) {
      initial = 1
    }
    if (!duration) {
      duration = 1000
    }
    if (!step) {
      step = 1
    }
    if (!roundto) {
      roundto = 1
    }
  }
</script>

<div use:styleable={$component.styles} class="spectrum-Heading {sizeClass}">
  {#key key}
  <Countup
    initial={parseInt(initial)}
    value={parseInt(value)}
    {duration}
    {step}
    {roundto}
    {format}
	/>
  {/key}
</div>
