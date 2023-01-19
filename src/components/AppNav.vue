<script>
export default {
  name: 'AppNav'
}
</script>

<template>
  <nav class="navbar navbar-expand-sm navbar-light bg-light border-bottom">
    <div class="container">
      <a class="navbar-brand" href="/">Navbar</a>
      <button class="navbar-toggler d-lg-none" type="button" data-bs-toggle="collapse" data-bs-target="#mainNav"
        aria-controls="mainNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="mainNav">
        <ul class="navbar-nav ms-auto mt-2 mt-lg-0">
          <li class="nav-item">
            <a class="nav-link active" href="/" aria-current="page">Home <span
                class="visually-hidden">(current)</span></a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Blog</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">Contacts</a>
          </li>
        </ul>

      </div>
    </div>
  </nav>

</template>

<style lang="scss" scoped>

</style>