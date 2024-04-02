<script lang="ts">
  import { browser } from '$app/environment'
  import {
    arrow,
    autoUpdate,
    computePosition,
    flip,
    offset,
    shift
  } from '@floating-ui/dom'
  import {
    AppShell,
    Modal,
    Toast,
    initializeStores,
    storePopup
  } from '@skeletonlabs/skeleton'
  import '../app.pcss'

  initializeStores()
  storePopup.set({ computePosition, autoUpdate, offset, shift, flip, arrow })

  /**
   * Init authentication
   */

  /**
   * UI loader
   */

  // To improve the UX while the app is loading on mainnet we display a spinner which is attached statically in the index.html files.
  // Once the authentication has been initialized we know most JavaScript resources has been loaded and therefore we can hide the spinner, the loading information.
  $: (() => {
    if (!browser) {
      return
    }

    const spinner = document.querySelector('body > #app-spinner')
    spinner?.remove()
  })()
</script>

<Modal position="items-start" class="*:max-h-full" />

<Toast position="br" width="max-w-xl w-full" zIndex="z-[10000]" />

<AppShell regionPage="scroll-smooth" scrollbarGutter="stable both-edges">
  <slot />
</AppShell>
