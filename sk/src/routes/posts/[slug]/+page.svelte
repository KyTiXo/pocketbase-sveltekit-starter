<script lang="ts">
  import ImgModal from "$lib/pocketbase/ImgModal.svelte";
  import { client } from "$lib/pocketbase/index.js";

  const { data } = $props();
  const record = $derived(data.record);
  $effect(() => {
    data.metadata.title = data.metadata.headline = record.title;
  });
</script>

<article class="prose lg:prose-xl">
  <pre class="body">{record.body}</pre>
  <h1>title</h1>
  {#each record.files ?? [] as file, index}
    {@const src = client.files.getUrl(record, file)}
    {@const title = `image ${index + 1} for: ${record.title}`}
    <!-- <img {src} alt={title} {title} /> -->
    <ImgModal {record} filename={file} />
  {/each}
</article>
