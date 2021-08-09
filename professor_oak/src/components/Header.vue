<template>
  <div class="container p-5">
    <div class="row">
      <div class="col-lg-6">
        <nav class="my_nav navbar">
          <div class="container-fluid">
            <form class="d-flex">
              <input class="form-control me-2" type="search" placeholder="Search a Pokémon" aria-label="Search">
              <button class="btn btn-outline-success" type="submit">
                <i class="bi bi-search"></i>
              </button>
            </form>
          </div>
        </nav>
      </div>

      <div class="col-lg-6">
        <nav class="my_nav navbar navbar-nav navbar-collapse">
          <div class="container-fluid">
            <span class="navbar-text">Gotta catch 'em all!</span>

             <li class="nav-item dropdown">
                <a class="nav-link dropdown-toggle" 
                   data-bs-toggle="dropdown" 
                   href="#" role="button" 
                   aria-expanded="false">
                    Filter by type
                  </a>
                  
                <ul class="dropdown-menu">
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
    </div>
  </div>
</template>


<script>

export default {
    name:'Header',
}
</script>


<style lang="scss" scoped>
.debug {
  color: var(--red);
}

.my_nav {
  background-color: var(--transparent-grey);
  backdrop-filter: blur(5px);

  border: 1px solid var(--transparent-grey);
  border-radius: 6px;
}
</style>