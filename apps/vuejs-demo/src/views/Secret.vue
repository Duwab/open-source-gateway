<template>
  <div>
    <h1>This is a secret about page. You should only be able to see this if you are authenticated.</h1>
    <h3>This is what my token looks like:</h3>
    <pre>{{ $keycloak.tokenParsed }}</pre>
  </div>
</template>
<style scoped>
  pre {
    text-align: left;
    max-width: 400px;
    margin: auto;
  }
</style>
