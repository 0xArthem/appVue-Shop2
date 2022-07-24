<template>
  <nav class="navbar navbar-light navbar__text">
    <div class="container-fluid navbar__text__container">
      <span class="navbar-text">
        <em class="fas fa-caret-right"></em>
        Offre promotionnelle de -50% du 14 au 27 juillet 2022
      </span>
    </div>
  </nav>

  <nav class="navbar navbar-expand-lg navbar-light bg-dark">
    <div class="container-fluid">
      <button
        class="navbar-toggler"
        type="button"
        data-mdb-toggle="collapse"
        data-mdb-target="#navbarCenteredExample"
        aria-controls="navbarCenteredExample"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <em class="fas fa-bars"></em>
      </button>
      <div
        class="collapse navbar-collapse justify-content-center"
        id="navbarCenteredExample"
      >
        <ul class="navbar-nav mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="#">
              <router-link to="/"><em class="fas fa-home text-light"></em></router-link>
            </a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
  <router-view/>
</template>

<style scoped>
#app {
  font-family: Roboto, Helvetica, Arial, sans-serif;
}
nav a.router-link-exact-active {
  color: #42b983;
}

.navbar__text{
  background-color: #fbfbfb;
}
.navbar__text__container{
  height:30px !important;
  display:flex !important;
  justify-content: center !important;
}
.navbar-text{
  color: #262626;
  margin-top:-10px;
  font-family: 'Tinos', serif;
  font-size:17px;
  letter-spacing: 1px;
}
.fa-caret-right{
  margin-right:3px;
  color: #42b983;
}
</style>
<style>
#app{
    overflow-x: hidden;
}
</style>