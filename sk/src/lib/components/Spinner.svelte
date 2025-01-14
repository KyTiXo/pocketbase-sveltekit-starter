<script lang="ts" context="module">
  import { writable } from "svelte/store";

  // returns a store that:
  // starts out false
  // becomes true when the async function f starts running
  // becomes false when f resolves (or rejects)
  export function activityStore<T>(f: (t: T) => Promise<any>) {
    const store = writable(false);
    async function run(data: T) {
      try {
        store.set(true);
        return await f(data);
      } finally {
        store.set(false);
      }
    }
    return { ...store, run };
  }
</script>

<script lang="ts">
  let { active }: { active: boolean } = $props();
</script>

<!--
  @component
  ```svelte
  <Spinner
  ```
 -->
<span class="loading loading-dots loading-md hidden" class:inline-block={active}
></span>
