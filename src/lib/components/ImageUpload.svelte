<script>
    import Upload from 'virtual:icons/ph/upload-fill';

    let show = false;
    let upload;
    export let file;
    let preview;
    let size;

    let width;
    let height;

    export let callback;

    function onChange() {
        show = true;

        const reader = new FileReader();
        reader.addEventListener("load", function () {
            let img = new Image();

            img.onload = function () {
                width = img.width;
                height = img.height;

                size.innerHTML = `${width}x${height}`;

                if (callback) {
                    callback(width, height);
                }
            };

            img.src = reader.result;

            preview.src = reader.result;
        })
        reader.readAsDataURL(file.files[0]);
    }

    function onDragOver(ev) {
        ev.preventDefault();
    }

    function onDrop(ev) {
        ev.preventDefault();

        file.files = ev.dataTransfer.files;
        onChange();
    }
</script>


<label bind:this={upload} on:dragover={onDragOver} on:drop={onDrop} class="border-2 rounded-md border-zinc-500 size-96 text-center block m-5">
    <input bind:this={file} on:change={onChange} type="file" accept="image/*" id="upload" hidden>
    <div id="preview" class="size-full flex justify-center items-center flex-col relative">
        {#if show}
            <img bind:this={preview} src="" alt="Preview" class="size-full object-contain">
            <span bind:this={size} class="text-zinc-400 bg-zinc-600 absolute left-0 bottom-0 p-0.5 rounded-tr">resolution</span>
        {:else}
            <Upload class="text-zinc-500 text-8xl" />
            <p class="text-zinc-500 text-lg font-bold">Drag & drop or click here to upload</p>
        {/if}
    </div>
</label>
