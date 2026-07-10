<script>
    import gh_icon from '$lib/images/gh_cat_white.png';
    const projects = [
        {
            name: "space sonification",
            width: "25vw",
            height: "25vh",
            technologies: ["vue","threejs", "pinia", "typescript", "expressjs"],
            description: "A web app for translating NASA's sonification audio files and bring them to life with three js with interactivity of the cosmos that react to audio frequency data.",
            status: "in progress",
            repo_link: "https://github.com/adamkasten/space_sonification"
        },
        {
            name: "hamburg audio utility",
            width: "25vw",
            height: "25vh",
            technologies: ["vue", "expressjs", "ffmpeg", "typescript"],
            description: "A utility web app allowing users to upload a video or audio file and convert them into an entirely new format using ffmpeg. This is a local utility that is not hosted on the web.",
            status: "done",
            repo_link: "https://github.com/adamkasten/hamburg_utils"
        },
        {
            name: "space traders api dashboard",
            width: "25vw",
            height: "25vh",
            technologies: ["vue", "expressjs", "axios", "typescript"],
            description: "A dashboard for the api game space traders.",
            status: "in progress",
            repo_link: "https://github.com/adamkasten/spacetraders"
        }
    ]
</script>

<div class="content_container">
    <h1 class="site_headers space_grotesk_norm">projects</h1>
        <div class="content_container_child space_grotesk_norm" id="projects">
            {#each projects as project}
                <div class="project_container">
                    <span class="project_name">{project.name}</span>
                    <p class="project_description">{project.description}</p>
                    <ul>
                        {#each project.technologies as tech}
                            <li class="project_technologies">{tech}</li>
                        {/each}
                    </ul>

                    {#if project.status === "done"}<span class="project_status" style="color: greenyellow;"><a href="{project.repo_link}" target="_blank"><img src="{gh_icon}" alt="github white icon"/></a>{project.status}</span>
                    {:else}
                    <span class="project_status"><a href="{project.repo_link}" target="_blank"><img src="{gh_icon}" alt="github white icon"/></a>{project.status}</span>
                    {/if}

                </div>
            {/each}
	</div>
</div>


<style>

#projects {
    gap: 20px;
    background: none;
    padding: 0;
    flex-direction: row;
    max-width: 100vw;
    flex-wrap: wrap;
    margin: 2vw;
}

.project_container {
    padding: 20px;
    background: var(--dark_amethyst);
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    width: 49%;
}

.project_name {
    text-transform: uppercase;
}

.project_status {
    padding-top: 2em;
    justify-self: right;
    align-self: self-end;
    margin-top: auto;
}

.project_description {
    padding: 1.5em 0;
    width: 75%;
}

ul {
    display: flex;
    gap: 1em;
    align-items: center;
    margin-top: auto;
    list-style: none;
    padding: 0;
}

li {
    border: 2px solid var(--indigo);
    padding: 0.25em 1em;
    background: var(--bg);
    border-radius: 10px;
}

img {
    height: 2em;
    width: 2em;
    justify-self: right;
    margin: .5em 0;
}

	@media (width <= 1300px) {

	#projects {
		flex-direction: column;
        width: 96dvw;
	}

    ul {
        gap: 0.5em;
        flex-wrap: wrap;
    }

    .project_description {
        width: 100%;
    }

    .project_container {
        width: 100%;
    }

}

</style>
