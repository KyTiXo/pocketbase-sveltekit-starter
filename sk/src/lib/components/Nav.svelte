<script lang="ts">
  import { base } from "$app/paths";
  import { page } from "$app/state";
  const links = [
    ["/", "Home"],
    ["/posts/", "Posts"],
    ["/hello/", "Hello"],
  ];
</script>

<div class="flex flex-col w-full">
  <!-- Top navbar (always visible) -->
  <nav class="navbar justify-between gap-4 bg-base-300">
    <!-- Logo -->
    <a href={`${base}/`} class="btn btn-ghost text-lg">
      <i class="fa fa-search w-4 text-primary-content" aria-hidden="true"></i>
      <!-- <img alt="Logo" src="/logo.svg" class="w-4" /> -->
      Company
    </a>

    <!-- Search -->
    <div class="join w-full max-w-xl hidden sm:inline-flex">
      <!-- Search options -->
      <select class="select select-sm select-bordered join-item">
        <option selected>Good potions</option>
        <option>Bad potions</option>
        <option>Illegal potions</option>
      </select>

      <!-- Search input -->
      <input
        class="join-item input input-sm input-bordered w-full"
        type="text"
        placeholder="Search"
      />

      <!-- Search button -->
      <button class="join-item btn btn-sm btn-primary text-success-content">
        <i class="fa fa-search" aria-hidden="true"></i>
      </button>
    </div>

    <!-- Menu (Desktop) -->
    <div class="shrink-0 hidden md:flex gap-2">
      {#each links as [path, label]}
        {@const active = page.url.pathname == path}
        <!-- <a  class:active>{label}</a> -->
        <a
          href={`${base}${path}`}
          class="btn btn-sm btn-ghost"
          class:btn-active={active}>{label}</a
        >
        <!-- <a class="btn btn-sm btn-primary">
			Log in
			<i class="fa-solid fa-right-to-bracket" aria-hidden="true"></i>
		</a> -->
      {/each}
      <slot />
    </div>

    <!-- Menu (Mobile) -->
    <div class="dropdown dropdown-end md:hidden">
      <button class="btn btn-ghost">
        <i class="fa-solid fa-bars text-lg"></i>
      </button>

      <ul
        tabindex="0"
        class="dropdown-content menu z-[1] bg-base-200 p-4 rounded-box shadow w-56 gap-2"
      >
        <li><a>Create Account</a></li>
        <a class="btn btn-primary btn-sm">
          Log in
          <i class="fa fa-arrow-right text-xs" aria-hidden="true"></i>
        </a>
      </ul>
    </div>
  </nav>

  <!-- Botton navbar (mobile only) -->
  <nav class="navbar sm:hidden bg-base-200 border-neutral">
    <!-- Search -->
    <div class="join w-full">
      <!-- Search options -->
      <select class="select select-sm select-bordered join-item">
        <option selected>Good potions</option>
        <option>Bad potions</option>
        <option>Illegal potions</option>
      </select>

      <!-- Search input -->
      <input
        class="join-item input input-sm input-bordered w-full"
        type="text"
        placeholder="Search"
      />

      <!-- Search button -->
      <button class="join-item btn btn-sm btn-primary text-success-content">
        <i class="fa fa-search" aria-hidden="true"></i>
      </button>
    </div>
  </nav>
</div>
