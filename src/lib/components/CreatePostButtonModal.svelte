<script>
    import { currentUser, pb } from '$lib/pocketbase';

    let caption = '';
    const formData = new FormData();

    const handleFileChange = (event) => {
        for (let file of event?.target?.files) {
            formData.append('photo', file);
        }
    };

    const handleCreatePost = async() => {
        formData.append('caption', caption);
        formData.append('user', $currentUser.id);
        await pb.collection('posts').create(formData);
        caption = '';
    }
</script>

{#if $currentUser}
    <div class="flex justify-center">
    <!-- The button to open modal -->
    <label for="my-modal-4" class="btn btn-primary">Create post</label>

    <!-- Put this part before </body> tag -->
    <input type="checkbox" id="my-modal-4" class="modal-toggle" />
    <label for="my-modal-4" class="modal cursor-pointer">
        <label class="modal-box relative" for="">
        <div class="space-y-4">
            <h3 class="text-lg font-bold">Create post</h3>
            <div class="form-control">
                <label class="label">
                    <span class="label-text">Caption</span>
                </label>
                <textarea class="textarea textarea-bordered h-24" bind:value={caption}></textarea>
            </div>
                <input type="file" class="file-input file-input-bordered w-full max-w-xs" 
                on:change={handleFileChange}
                />
                <label for="my-modal-4" class="btn btn-block btn-primary" on:click={handleCreatePost}>Create post                
                </label>
        </div>
        </label>
    </label>
    </div>

{/if}

