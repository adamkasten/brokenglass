<script>
	import { smootherstep } from "three/src/math/MathUtils.js";
  import { page } from '$app/state';


  function hover_animation() {

  }

  function scroll_to_content() {
    const content = document.getElementById("home_content");
    content?.scrollIntoView({
      behavior: "smooth",
      block: "center",
    });
  }

</script>

<nav class="crumbs">
  <ol>
    <a href="/" class="nav_button space_grotesk_norm"><li class="crumb">home</li></a>
    <a href="/projects" class="nav_button space_grotesk_norm"><li class="crumb">projects</li></a>
    <a href="/contact" class="nav_button space_grotesk_norm"><li class="crumb">contact</li></a>
  </ol>
  {#if page.url.pathname === '/'}
  <button type="button" id="scroll_btn" onclick={scroll_to_content}>&#8623;</button>
  {/if}
</nav>

<style>
  nav {
    background: var(--dark_amethyst);
    color: var(--creamy);
    width: 200px;
    flex-shrink: 0;
    z-index: 99;
  }
  .crumbs ol {
    list-style-type: none;
    padding-left: 0;
    position: sticky;
    top: 0;
    z-index: 2;
  }

  .nav_button {
    display: inline-block;
    width: 100%;
    height: auto;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 2rem;
    padding: 20px 30px;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    line-height: 1;
    text-overflow: ellipsis;
    border-style: none;
    font-weight: bold;
    transition: all .3s ease-in-out;
    background: rgba(39, 1, 65, 0.014);
    
  }
  .crumb {
    list-style-type: none;
    padding-left: 0;
    transition: all .3s ease-in-out;
  }

  .nav_button:hover {
    background-color: var(--indigo);
    transition: all .3s ease-in-out;
  }

  #scroll_btn {
    display: inline-block;
    width: 100%;
    height: auto;
    text-overflow: ellipsis;
    white-space: nowrap;
    font-size: 2rem;
    padding: 10px 30px;
    cursor: pointer;
    text-align: center;
    text-decoration: none;
    line-height: 1;
    text-overflow: ellipsis;
    border-style: none;
    font-weight: bold;
    transition: all .3s ease-in-out;
    background: rgba(39, 1, 65, 0.014);
    background: var(--accent);
    position: relative;
    z-index: 0;
}

  	@media (width <= 1300px) {
      nav {
        width: 100dvw;
        position: sticky;
        top: 0;
      }

      .nav_button {
        padding: 10px 10px;
        font-size: 1.5rem;
      }
}
</style>