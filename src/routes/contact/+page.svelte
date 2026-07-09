<script>
    import Navbar from '../../lib/Navbar.svelte';
</script>



<div class="content_container space_grotesk_norm">
<h1 class="site_headers space_grotesk_norm">contact</h1>
    <form action="https://api.web3forms.com/submit" method="POST">
      <input type="hidden" name="access_key" value="507d97fb-4fae-4f4d-908c-edb3d99ab003">
        <label>
            <p>name</p>
            <input name="name" type="text" placeholder="steve wozniak" required>
        </label>
        <label>
            <p>email</p>
            <input name="email" type="email" placeholder="wile@acme.com" required>
        </label>
        <label>
            <p>message</p>
            <textarea name="message" placeholder="type your message here..." rows="5" cols="5" required></textarea>
        </label>
        <button type="submit">submit</button>
    </form>
</div>

<style>
    form {
        display: flex;
        justify-content: flex-end;
        flex-direction: column;
        background: var(--dark_amethyst);
        color: var(--creamy);
        padding: 50px;
        text-align: left;
        margin-left: 2em;
        gap: 1em;
        border-radius: 10px;
        min-width: 25vw;
        max-width: 50vw;
        align-self: center;
    }

    form label {
        flex: 1;
    }

    textarea {
        background: var(--bg);
        border: none;
        border-radius: 10px;
        min-width: 100%;
    }

    button {
        cursor: pointer;
        padding: 20px;
        background: var(--indigo);
        border-radius: 10px;
        min-width: 100%;
    }

    input {
        background: var(--bg);
        border: none;
        border-radius: 5px;
        min-width: 100%;
        padding: 10px;
    }

    @media (width <= 1300px) {
        form {
            max-width: 100dvw;
            padding: 10px;
            margin-left: .5em;
        }
    }
</style>
