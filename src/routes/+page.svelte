<script>
    import ImageUpload from "$lib/components/ImageUpload.svelte";
    import Jimp from "jimp";


    let resX;
    let resY;

    let image1;
    let image2;

    let image1uploaded = false;
    let image2uploaded = false;

    let image1width;
    let image1height;

    let image2width;
    let image2height;

    let resButton1;
    let resButton2;

    function image1Set(image, width, height) {
        resButton1.disabled = false;

        image1 = image;

        image1width = width;
        image1height = height;

        image1uploaded = true;
    }

    function image2Set(image, width, height) {
        resButton2.disabled = false;

        image2 = image;

        image2width = width;
        image2height = height;

        image2uploaded = true;
    }

    function image1Resolution() {
        resX = image1width;
        resY = image1height;
    }

    function image2Resolution() {
        resX = image2width;
        resY = image2height;
    }

    function generate() {
        //let foreground = Jimp.read(image1);
        //let background = Jimp.read(image2);

        //foreground.cover(resX, resY, Jimp.RESIZE_BILINEAR || Jimp.HORIZONTAL_ALIGN_CENTER || Jimp.VERTICAL_ALIGN_MIDDLE);


    }
</script>


<h1 class="text-white text-center text-5xl">
    Doom Transition GIF Generator
</h1>

<div class="flex justify-center">
    <div>
        <h2 class="text-white text-center text-xl">Foreground</h2>
        <ImageUpload callback={image1Set} />
    </div>
    <div>
        <h2 class="text-white text-center text-xl">Background</h2>
        <ImageUpload callback={image2Set} />
    </div>
</div>

<div class="bg-zinc-700 w-fit p-4 rounded-md text-center">
    <input bind:value={resX} type="number" class="no-spinner rounded bg-zinc-600 text-white w-14 px-1">
    <span class="text-white">x</span>
    <input bind:value={resY} type="number" class="no-spinner rounded bg-zinc-600 text-white w-14 px-1">
    <span class="text-white">px</span>
    <br>
    <div class="my-2">
        <button bind:this={resButton1} on:click={image1Resolution} disabled class="text-white bg-zinc-600 py-1 rounded-l px-2 hover:bg-zinc-500 disabled:bg-zinc-500">Use foreground resolution</button><!--
        --><button bind:this={resButton2} on:click={image2Resolution} disabled class="text-white bg-zinc-600 py-1 rounded-r px-2 hover:bg-zinc-500 disabled:bg-zinc-500">Use background resolution</button>
    </div>
    <button disabled={!(resX > 0 && resY > 0 && image1uploaded && image2uploaded)} class="text-white bg-orange-500 hover:bg-orange-400 disabled:bg-orange-400 py-1 px-2 rounded">Generate</button>
</div>
