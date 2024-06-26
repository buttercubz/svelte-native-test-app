<script lang="ts">
  import { HomeToolBar } from "@/lib/components/blocks/HomeToolBar";
  import {
    Page,
    BlockTitle,
    List,
    ListItem,
    Radio,
    Toggle,
    Block,
  } from "konsta/svelte";
  import { HomeNavBar } from "@/lib/components/blocks/HomeNavBar";
  import { Navigation, Pagination } from "swiper/modules";
  import { createEventDispatcher, onMount } from "svelte";
  import * as Drawer from "$lib/components/ui/drawer";
  import { toggleMode, mode } from "mode-watcher";
  import Swiper from "swiper";

  type Tabs = "chats" | "status" | "groups" | "calls";

  let tab: Tabs = "chats";

  let swiper: Swiper;

  const titles = {
    chats: "WhatsApp",
    status: "Novedades",
    groups: "Comunidades",
    calls: "Llamadas",
  };

  const getTab: Record<number, Tabs> = {
    0: "chats",
    1: "status",
    2: "groups",
    3: "calls",
  };

  const getIndexTab: Record<Tabs, number> = {
    chats: 0,
    status: 1,
    groups: 2,
    calls: 3,
  };

  $: title = titles[tab];
  $: tabIndex = getIndexTab[tab];
  $: swiper?.slideTo?.(tabIndex);

  let openSettings = false;

  let hide = false;

  export let theme: "ios" | "material";

  const dispatch = createEventDispatcher<{ theme: "ios" | "material" }>();

  onMount(() => {
    swiper = new Swiper(".swiper", {
      modules: [Navigation, Pagination],
    });

    swiper.on("activeIndexChange", (e) => (tab = getTab[e.activeIndex]));
  });
</script>

<Page class="ios:pb-[63px] material:pb-[45px]">
  <HomeNavBar
    on:open={({ detail }) => (openSettings = detail === "menu")}
    on:search={({ detail }) => (hide = detail)}
    {title}
    {theme}
  />

  <div class="swiper">
    <div class="swiper-wrapper">
      <div class="swiper-slide">
        <BlockTitle>Simple List</BlockTitle>
        <List>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong List</BlockTitle>

        <List strong>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline List</BlockTitle>

        <List strong outline>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Inset List</BlockTitle>

        <List strong inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline Inset List</BlockTitle>

        <List strong outline inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Simple Links List</BlockTitle>

        <List strongIos outlineIos>
          <ListItem title="Link 1" link />
          <ListItem title="Link 2" link />
          <ListItem title="Link 3" link />
        </List>

        <BlockTitle>Data list, with icons</BlockTitle>

        <BlockTitle>Links</BlockTitle>

        <BlockTitle>Links, Header, Footer</BlockTitle>

        <BlockTitle>Links, no icons</BlockTitle>
        <List strongIos outlineIos>
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="John Doe" />
          <ListItem groupTitle title="Group title Here" />
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="Jenna Smith" />
        </List>

        <BlockTitle>Grouped with sticky titles</BlockTitle>

        <BlockTitle class="text-2xl">Media Lists</BlockTitle>
        <Block>
          <p>
            Media Lists are almost the same as Data Lists, but with a more
            flexible layout for visualization of more complex data, like
            products, services, user, etc.
          </p>
        </Block>

        <BlockTitle>Songs</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Yellow Submarine"
            after="$15"
            subtitle="Beatles"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Don't Stop Me Now"
            after="$22"
            subtitle="Queen"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-2.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Billie Jean"
            after="$16"
            subtitle="Michael Jackson"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
        </List>
        <BlockTitle>Mail App</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="17:14"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="17:11"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="16:48"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="15:32"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
        </List>
      </div>
      <div class="swiper-slide">
        <BlockTitle>Simple List</BlockTitle>
        <List>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong List</BlockTitle>

        <List strong>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline List</BlockTitle>

        <List strong outline>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Inset List</BlockTitle>

        <List strong inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline Inset List</BlockTitle>

        <List strong outline inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Simple Links List</BlockTitle>

        <List strongIos outlineIos>
          <ListItem title="Link 1" link />
          <ListItem title="Link 2" link />
          <ListItem title="Link 3" link />
        </List>

        <BlockTitle>Data list, with icons</BlockTitle>

        <BlockTitle>Links</BlockTitle>

        <BlockTitle>Links, Header, Footer</BlockTitle>

        <BlockTitle>Links, no icons</BlockTitle>
        <List strongIos outlineIos>
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="John Doe" />
          <ListItem groupTitle title="Group title Here" />
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="Jenna Smith" />
        </List>

        <BlockTitle>Grouped with sticky titles</BlockTitle>

        <BlockTitle class="text-2xl">Media Lists</BlockTitle>
        <Block>
          <p>
            Media Lists are almost the same as Data Lists, but with a more
            flexible layout for visualization of more complex data, like
            products, services, user, etc.
          </p>
        </Block>

        <BlockTitle>Songs</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Yellow Submarine"
            after="$15"
            subtitle="Beatles"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Don't Stop Me Now"
            after="$22"
            subtitle="Queen"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-2.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Billie Jean"
            after="$16"
            subtitle="Michael Jackson"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
        </List>
        <BlockTitle>Mail App</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="17:14"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="17:11"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="16:48"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="15:32"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
        </List>
      </div>
      <div class="swiper-slide">
        <BlockTitle>Simple List</BlockTitle>
        <List>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong List</BlockTitle>

        <List strong>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline List</BlockTitle>

        <List strong outline>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Inset List</BlockTitle>

        <List strong inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline Inset List</BlockTitle>

        <List strong outline inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Simple Links List</BlockTitle>

        <List strongIos outlineIos>
          <ListItem title="Link 1" link />
          <ListItem title="Link 2" link />
          <ListItem title="Link 3" link />
        </List>

        <BlockTitle>Data list, with icons</BlockTitle>

        <BlockTitle>Links</BlockTitle>

        <BlockTitle>Links, Header, Footer</BlockTitle>

        <BlockTitle>Links, no icons</BlockTitle>
        <List strongIos outlineIos>
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="John Doe" />
          <ListItem groupTitle title="Group title Here" />
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="Jenna Smith" />
        </List>

        <BlockTitle>Grouped with sticky titles</BlockTitle>

        <BlockTitle class="text-2xl">Media Lists</BlockTitle>
        <Block>
          <p>
            Media Lists are almost the same as Data Lists, but with a more
            flexible layout for visualization of more complex data, like
            products, services, user, etc.
          </p>
        </Block>

        <BlockTitle>Songs</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Yellow Submarine"
            after="$15"
            subtitle="Beatles"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Don't Stop Me Now"
            after="$22"
            subtitle="Queen"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-2.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Billie Jean"
            after="$16"
            subtitle="Michael Jackson"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
        </List>
        <BlockTitle>Mail App</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="17:14"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="17:11"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="16:48"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="15:32"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
        </List>
      </div>
      <div class="swiper-slide">
        <BlockTitle>Simple List</BlockTitle>
        <List>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong List</BlockTitle>

        <List strong>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline List</BlockTitle>

        <List strong outline>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Inset List</BlockTitle>

        <List strong inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Strong Outline Inset List</BlockTitle>

        <List strong outline inset>
          <ListItem title="Item 1" />
          <ListItem title="Item 2" />
          <ListItem title="Item 3" />
        </List>

        <BlockTitle>Simple Links List</BlockTitle>

        <List strongIos outlineIos>
          <ListItem title="Link 1" link />
          <ListItem title="Link 2" link />
          <ListItem title="Link 3" link />
        </List>

        <BlockTitle>Data list, with icons</BlockTitle>

        <BlockTitle>Links</BlockTitle>

        <BlockTitle>Links, Header, Footer</BlockTitle>

        <BlockTitle>Links, no icons</BlockTitle>
        <List strongIos outlineIos>
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="John Doe" />
          <ListItem groupTitle title="Group title Here" />
          <ListItem link title="Ivan Petrov" />
          <ListItem link title="Jenna Smith" />
        </List>

        <BlockTitle>Grouped with sticky titles</BlockTitle>

        <BlockTitle class="text-2xl">Media Lists</BlockTitle>
        <Block>
          <p>
            Media Lists are almost the same as Data Lists, but with a more
            flexible layout for visualization of more complex data, like
            products, services, user, etc.
          </p>
        </Block>

        <BlockTitle>Songs</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Yellow Submarine"
            after="$15"
            subtitle="Beatles"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-1.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Don't Stop Me Now"
            after="$22"
            subtitle="Queen"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-2.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
          <ListItem
            chevronMaterial={false}
            link
            title="Billie Jean"
            after="$16"
            subtitle="Michael Jackson"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          >
            <img
              class="ios:rounded-lg material:rounded-full ios:w-20 material:w-10"
              slot="media"
              src="https://cdn.framework7.io/placeholder/people-160x160-3.jpg"
              width="80"
              alt="demo"
            />
          </ListItem>
        </List>
        <BlockTitle>Mail App</BlockTitle>
        <List strongIos outlineIos>
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="17:14"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="17:11"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="Facebook"
            after="16:48"
            subtitle="New messages from John Doe"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
          <ListItem
            chevronMaterial={false}
            link
            title="John Doe (via Twitter)"
            after="15:32"
            subtitle="John Doe (@_johndoe) mentioned you on Twitter!"
            text="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Nulla sagittis tellus ut turpis condimentum, ut dignissim lacus tincidunt. Cras dolor metus, ultrices condimentum sodales sit amet, pharetra sodales eros. Phasellus vel felis tellus. Mauris rutrum ligula nec dapibus feugiat. In vel dui laoreet, commodo augue id, pulvinar lacus."
          />
        </List>
      </div>
    </div>
  </div>

  <HomeToolBar {tab} {hide} on:tab={({ detail }) => (tab = detail)} />

  <Drawer.Root bind:open={openSettings}>
    <Drawer.Content>
      <List strong inset>
        <ListItem label title="iOS Theme">
          <Radio
            onChange={() => dispatch("theme", "ios")}
            checked={theme === "ios"}
            component="div"
            slot="media"
          />
        </ListItem>

        <ListItem label title="Material Theme">
          <Radio
            onChange={() => dispatch("theme", "material")}
            checked={theme === "material"}
            component="div"
            slot="media"
          />
        </ListItem>
      </List>

      <List strong inset>
        <ListItem title="Dark Mode" label>
          <Toggle
            onChange={() => toggleMode()}
            checked={$mode === "dark"}
            component="div"
            slot="after"
          />
        </ListItem>
      </List>
    </Drawer.Content>
  </Drawer.Root>
</Page>
