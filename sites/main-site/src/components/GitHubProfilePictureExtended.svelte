<script lang="ts">
    import GitHubProfilePicture from "./GitHubProfilePicture.svelte";

    export let username: string;
    export let affiliation: string = "";
    export let size: number = 50;
    export let wrapperClasses: string = "";
    export let labelClasses: string = "";
    export let containerQuery: boolean = false;
    export let imgClasses: string = "";

    const affiliation_str =
        affiliation.length > 0
            ? `<div class="small"><abbr class="small d-block affiliation" data-bs-placement="bottom" data-bs-toggle="tooltip" title="${affiliation}">${affiliation}</abbr></div>`
            : "";
    labelClasses = affiliation.length > 0 ? labelClasses + " small" : labelClasses;
</script>

<GitHubProfilePicture
    wrapperClasses={"d-block " + wrapperClasses}
    linkClasses="btn btn-light rounded-pill mb-2 p-0 d-flex align-items-center"
    image={"https://github.com/" + username + ".png"}
    name={username}
    circle={true}
    size={Math.max(size, 25)}
    {containerQuery}
    {imgClasses}
>
    <div class={"ms-2 pe-2 text-start d-flex flex-column profile-name " + labelClasses}>
        <div class={"ps-2 pe-3 " + labelClasses}>
            <slot>
                @{username}
            </slot>
            {@html affiliation_str}
        </div>
    </div></GitHubProfilePicture
>

<style lang="scss">
    :global(.profile-name p) {
        margin-bottom: 0;
    }
    :global(.affiliation) {
        max-width: 15rem;
        overflow: hidden;
    }
    :global(.github-link:hover .affiliation) {
        max-width: 100%;
    }
</style>
