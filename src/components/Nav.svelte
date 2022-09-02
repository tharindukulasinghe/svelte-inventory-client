<script>
  export let segment;
</script>

<nav>
  <ul class="nav justify-content-center">
    <li>
      <a aria-current={segment === undefined ? "page" : undefined} href="."
        >Home</a
      >
    </li>
    <li>
      <a
        rel="prefetch"
        aria-current={segment === "items" ? "page" : undefined}
        href="items">Items</a
      >
    </li>
    <li>
      <a
        rel="prefetch"
        aria-current={segment === "inventory" ? "page" : undefined}
        href="inventory">Inventory</a
      >
    </li>
    <li>
      <a
        aria-current={segment === "summary" ? "page" : undefined}
        href="summary">Summary</a
      >
    </li>
  </ul>
</nav>

<style>
  nav {
    border-bottom: 1px solid rgba(255, 62, 0, 0.1);
    font-weight: 300;
    padding: 0 1em;
  }

  ul {
    margin: 0;
    padding: 0;
  }
  ul::after {
    content: "";
    display: block;
    clear: both;
  }

  li {
    font-weight: 600;
    margin-left: 10px;
  }

  [aria-current] {
    position: relative;
    display: inline-block;
  }

  [aria-current]::after {
    position: absolute;
    content: "";
    width: calc(100% - 1em);
    height: 2px;
    background-color: rgb(255, 62, 0);
    display: block;
    bottom: -1px;
  }

  a {
    text-decoration: none;
    padding: 1em 0.5em;
    display: block;
  }
</style>
