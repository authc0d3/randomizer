<script>
  let year = new Date().getFullYear();
</script>

<footer class="container">
  &copy; {year}
  <a href="https://programadorweb.dev" target="_blank">Antonio González</a> ~
  Made with <a href="https://svelte.dev/" target="_blank">Svelte</a>
</footer>

<style>
  footer {
    border-top: 1px solid #9c9c9c;
    color: #9c9c9c;
    text-align: center;
    margin-top: 25px;
    padding: 10px 5px;
  }

  footer a {
    color: #9c9c9c;
    text-decoration: none;
  }

  footer a:hover,
  footer a:active {
    color: orangered;
    text-decoration: underline;
  }
</style>
