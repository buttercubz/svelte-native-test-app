<script lang="ts">
  import { Router, Route } from "svelte-routing";
  import { ModeWatcher } from "mode-watcher";
  import { Device } from "@capacitor/device";
  import Login from "@/views/Login.svelte";
  import View from "@/views/View.svelte";
  import Home from "@/views/Home.svelte";
  import { App } from "konsta/svelte";
  import { onMount } from "svelte";

  let theme: "material" | "ios" = "material";

  const platforms = {
    web: "material",
    android: "material",
    ios: "ios",
  } as const;

  onMount(() => {
    Device.getInfo()
      .then(({ platform }) => {
        theme = platforms[platform];
      })
      .catch((e) => alert(`Device info error: ${e.message}`));
  });
</script>

<ModeWatcher track />

<Router>
  <App {theme} safeAreas>
    <Route path="/">
      <Home {theme} on:theme={({ detail }) => (theme = detail)} />
    </Route>

    <Route path="/login">
      <!-- <Home {theme} on:theme={({ detail }) => (theme = detail)} /> -->
      <Login />
    </Route>

    <Route path="/view">
      <View />
    </Route>
  </App>
</Router>
