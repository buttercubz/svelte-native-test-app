<script lang="ts">
  import { cn } from "@/lib/utils";
  import { Toolbar, Link } from "konsta/svelte";
  import {
    MessageSquareMore,
    CircleFadingPlus,
    Users,
    Phone,
  } from "lucide-svelte";
  import { createEventDispatcher } from "svelte";

  export let hide = false;

  export let tab: "chats" | "status" | "groups" | "calls";

  const dispatch = createEventDispatcher<{
    tab: "chats" | "status" | "groups" | "calls";
  }>();
</script>

{#if !hide}
  <Toolbar
    top={false}
    class={`left-0 ${
      false
        ? "ios:top-11-safe material:top-14-safe sticky"
        : "bottom-0 h-24 fixed"
    } w-full p-5`}
  >
    <Link
      toolbar
      class="flex flex-col items-center justify-center"
      onClick={() => dispatch("tab", "chats")}
    >
      <MessageSquareMore
        class={cn({ "bg-primary/15 rounded-lg": tab === "chats" })}
        size={32}
      />
      <p>Chats</p>
    </Link>

    <Link
      toolbar
      class="flex flex-col items-center justify-center"
      onClick={() => dispatch("tab", "status")}
    >
      <CircleFadingPlus
        class={cn({ "bg-primary/15 rounded-lg": tab === "status" })}
        size={32}
      />
      Novedades
    </Link>

    <Link
      toolbar
      class="flex flex-col items-center justify-center"
      onClick={() => dispatch("tab", "groups")}
    >
      <Users
        class={cn({ "bg-primary/15 rounded-lg": tab === "groups" })}
        size={32}
      />
      Comunidades
    </Link>

    <Link
      toolbar
      class="flex flex-col items-center justify-center"
      onClick={() => dispatch("tab", "calls")}
    >
      <Phone
        class={cn({ "bg-primary/15 rounded-lg": tab === "calls" })}
        size={32}
      />
      Llamadas
    </Link>
  </Toolbar>
{/if}
