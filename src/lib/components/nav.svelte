<script>
    export let location;
    export let text;
</script>

<div class="nav">
    <a href="{location}">{text} &#8594;</a>
</div>

<style>
    .nav {
      position: absolute;
      top: 20px;
      right: 10px;
      z-index: 100;
    }
    a {
      color: white;
      font-size: clamp(1rem, 1vw, 2rem);
      text-decoration: none;
      text-transform: uppercase;
      font-family: 'Roboto', sans-serif;
      border: 1px solid white;
      padding: 10px;
    }
  </style>