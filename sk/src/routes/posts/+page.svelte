<script lang="ts">
  import { base } from "$app/paths";
  import DateShow from "$lib/components/DateShow.svelte";
  import Image from "$lib/pocketbase/Image.svelte";
  import Link2Modal from "$lib/components/Link2Modal.svelte";
  import { client } from "$lib/pocketbase";
  import EditPage from "./[slug]/edit/+page.svelte";
  import LoginGuard from "$lib/components/LoginGuard.svelte";
  import Paginator from "$lib/pocketbase/Paginator.svelte";
  import Spinner, { activityStore } from "$lib/components/Spinner.svelte";

  const { data } = $props();
  const posts = $derived(data.posts);
  $effect(() => {
    data.metadata.title = data.metadata.headline = "Posts";
  });
  const store = activityStore(() =>
    client.send("/api/generate", { method: "post" })
  );
</script>

<LoginGuard>
  <Link2Modal component={EditPage}>
    {#snippet trigger(onclick)}
      <a href="{base}/posts/new/edit" class="button" {onclick}>
        New Post
        <i class="bx bx-tada bx-list-plus"></i>
      </a>
    {/snippet}
  </Link2Modal>
  <button type="button" onclick={store.run} disabled={$store}
    ><Spinner active={$store} />
    Generate a random post
  </button>
  {#snippet otherwise()}
    <p>Please Sign In to create/edit posts.</p>
  {/snippet}
</LoginGuard>

<Paginator store={posts} showIfSinglePage={true} />

<ul class="list bg-base-100 rounded-box shadow-md">
  <li class="p-4 pb-2 text-xs opacity-60 tracking-wide">
    Most played songs this week
  </li>

  {#each $posts.items as item}
    {@const [file] = item.files}
    {@const thumbnail = client.files.getUrl(item, file, { thumb: "100x100" })}
    <!-- <a href={`${base}/posts/${item.slug || item.id}`} class="post"> -->

    <li class="list-row">
      <div>
        <!-- svelte-ignore a11y_missing_attribute -->
        <img src={thumbnail} class="size-10 rounded-box" />
      </div>
      <div>
        <div>{item.title}</div>
        <div class="text-xs uppercase font-semibold opacity-60">
          <!-- {item.expand.user.name} -->
        </div>
      </div>
      <a
        href={`${base}/posts/${item.slug || item.id}`}
        aria-label="play"
        class="btn btn-square btn-ghost"
      >
        <svg
          class="size-[1.2em]"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          ><g
            stroke-linejoin="round"
            stroke-linecap="round"
            stroke-width="2"
            fill="none"
            stroke="currentColor"><path d="M6 3L20 12 6 21 6 3z"></path></g
          ></svg
        >
      </a>
      <button class="btn btn-square btn-ghost" aria-label="heart">
        <svg
          class="size-[1.2em]"
          xmlns="http://www.w3.org/2000/svg"
          viewBox="0 0 24 24"
          ><g
            stroke-linejoin="round"
            stroke-linecap="round"
            stroke-width="2"
            fill="none"
            stroke="currentColor"
            ><path
              d="M19 14c1.49-1.46 3-3.21 3-5.5A5.5 5.5 0 0 0 16.5 3c-1.76 0-3 .5-4.5 2-1.5-1.5-2.74-2-4.5-2A5.5 5.5 0 0 0 2 8.5c0 2.3 1.5 4.05 3 5.5l7 7Z"
            ></path></g
          ></svg
        >
      </button>
    </li>
    <!-- {/each} -->

    <!-- <DateShow date={item.updated} /> -->
    <!-- <Image record={item} {file} /> -->
    <!-- <div>
      <div>
        <i class="bx bx-calendar" title="on date"></i>
        {new Intl.DateTimeFormat(undefined, { dateStyle: "full" }).format(
          new Date(item.updated)
        )}
        {#if item.expand?.user?.name}
          <i class="bx bx-pen" title="author"></i>
          {item.expand.user.name}
        {/if}
      </div>
      <h2>{item.title}</h2>
    </div> -->
    <!-- </a> -->
    <!-- {:else}
  <div>No posts found. Create some.</div> -->
  {/each}
</ul>
<Paginator store={posts} showIfSinglePage={true} />
