<script lang="ts">
  import { Home, Library, Cog, type Icon as IconType } from "lucide-svelte";

  type MenuItem = {
    name: string;
    href: string;
    icon?: typeof IconType;
  };

  const menuItems: MenuItem[] = [
    {
      name: "Home",
      href: "/",
      icon: Home,
    },
    {
      name: "Posts",
      href: "/posts",
      icon: Cog,
    },
    {
      name: "Features",
      href: "/blog",
      icon: Library,
    },
  ];
</script>

{#each menuItems as item}
  {@const Icon = item.icon}
  <li>
    <a href={item.href}>
      {#if Icon}
        <Icon />
      {/if}
      <span>{item.name}</span>
    </a>
  </li>
{/each}
