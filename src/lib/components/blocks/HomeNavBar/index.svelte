<script lang="ts">
  import { Block, Chip, Navbar, Searchbar, Link } from "konsta/svelte";
  import { Camera, CameraResultType } from "@capacitor/camera";
  import {
    CameraIcon,
    Search,
    EllipsisVertical,
    MessageSquareMore,
    Image,
    Video,
    Link2,
    Headphones,
    FileText,
    PieChart,
  } from "lucide-svelte";
  import { createEventDispatcher } from "svelte";

  export let theme: string;
  export let title = "";

  let isSearch = false;

  const dispatch = createEventDispatcher<{ open: "menu" }>();

  const takePicture = async () => {
    const image = await Camera.getPhoto({
      quality: 90,
      allowEditing: true,
      resultType: CameraResultType.Uri,
    });

    // image.webPath will contain a path that can be set as an image src.
    // You can access the original file using image.path, which can be
    // passed to the Filesystem API to read the raw data of the image,
    // if desired (or pass resultType: CameraResultType.Base64 to getPhoto)
    var imageUrl = image.webPath;

    console.log(imageUrl);
  };
</script>

{#if isSearch}
  <Navbar title="Search" class="flex flex-col">
    <Searchbar
      onBlur={() => (isSearch = false)}
      disableButtonText="Cancel"
      slot="subnavbar"
      disableButton
      value=""
    />
  </Navbar>

  <div class="ios:-mt-9 material:-mt-7">
    <Block strongIos outlineIos>
      <Chip class="m-0.5 space-x-1">
        <MessageSquareMore size={16} />
        <span> No leidos </span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <Image size={16} />
        <span>Fotos</span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <Video size={16} />
        <span>Videos</span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <Link2 size={16} />
        <span>Enlaces</span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <Image size={16} />
        <span>GIF</span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <Headphones size={16} />
        <span> Audio </span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <FileText size={16} />
        <span> Documents </span>
      </Chip>
      <Chip class="m-0.5 space-x-1">
        <PieChart size={16} />
        <span>Encuestas</span>
      </Chip>
    </Block>
  </div>
{:else}
  <Navbar {title} large={theme === "ios"}>
    <div
      slot="right"
      class="flex flex-row ios:space-x-3 absolute ios:left-[19rem] material:left-[19rem]"
    >
      <Link navbar onClick={takePicture}>
        <CameraIcon />
      </Link>
      <Link navbar onClick={() => (isSearch = true)}>
        <Search />
      </Link>
      <Link navbar onClick={() => dispatch("open", "menu")}>
        <EllipsisVertical />
      </Link>
    </div>
  </Navbar>
{/if}
