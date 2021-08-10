<template>
  <div class="container p-1">
    <div class="row">
      <div class="col-lg-6">
        <nav class="my_nav navbar">
          <div class="container-fluid">
            <form class="d-flex">
              <input class="form-control me-2 opacity-75" type="search" placeholder="Search a Pokémon" aria-label="Search">
              <button class="btn btn-outline-success" type="submit">
                <i class="bi bi-search"></i>
              </button>
            </form>

            <li class="nav nav-item dropdown position-relative">
              <a class="nav-link link-success dropdown-toggle" 
                 data-bs-toggle="dropdown" 
                 href="#" role="button" 
                 aria-expanded="false">
                  Filter by type
              </a>
                  
              <ul class="dropdown-menu position-absolute mt-3 p-1 my_drpo-menu_color">
                <li><a class="dropdown-item" href="#">Normal</a></li>
                <li><a class="dropdown-item" href="#">Fire</a></li>
                <li><a class="dropdown-item" href="#">Water</a></li>
                <li><hr class="dropdown-divider"></li>
                <li><a class="dropdown-item" href="#">Other</a></li>
              </ul>
            </li>
          </div>
        </nav>
      </div>

      <div class="col-lg-6">
        <nav class="my_nav navbar navbar-nav navbar-collapse">
          <div class="container-fluid">
            <span class="navbar-text tag_line">Gotta catch 'em all!</span>

            <span class="btn btn-outline-success">
              <i class="bi bi-arrow-repeat me-2"></i>
              Surprise me
            </span>
          </div>
        </nav>
      </div>
    </div>
  </div>
</template>


<script>

export default {
    name:'Header',
}
</script>


<style lang="scss" scoped>
.my_nav {
  background-color: var(--transparent-grey);

  border: 1px solid var(--transparent-grey);
  border-radius: 6px;
}

.my_drpo-menu_color {
  background-color: var(--ultra-transparent-grey);
  backdrop-filter: blur(5px);
}

.dropdown-item:hover {
  background-color: var(--transparent-grey);
  border-radius: 50rem!important;
}

input:focus { 
  border-color: var(--greenBulba);
  box-shadow: 1px 1px 5px var(--greenBulba);
}

.tag_line {
  color: var(--greenBulba);
}
</style>