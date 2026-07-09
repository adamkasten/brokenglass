<script>

  function hover_animation() {

  }

</script>

<nav class="crumbs">
  <ol>
    <a href="/" class="nav_button space_grotesk_norm"><li class="crumb">home</li></a>
    <a href="/projects" class="nav_button space_grotesk_norm"><li class="crumb">projects</li></a>
    <a href="/contact" class="nav_button space_grotesk_norm"><li class="crumb">contact</li></a>
  </ol>
</nav>

<style>
  nav {
    background: var(--dark_amethyst);
    color: var(--creamy);
    width: 200px;
    flex-shrink: 0;
  }
  .crumbs ol {
    list-style-type: none;
    padding-left: 0;
    position: sticky;
    top: 0;
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

  	@media (width <= 1300px) {
      nav {
        width: 100dvw;
      }

      .nav_button {
        padding: 10px 10px;
        font-size: 1.5rem;
      }
}
</style>