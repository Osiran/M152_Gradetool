<template>
  <h1 class="m-3 title">Gradeing Tool</h1>
  <router-view />
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}

body {
  background: linear-gradient(324deg, #4e2e0e, #465668, #5fa2e3, #b02db9, #53e1b4, #e879e4);
  background-size: 1200% 1200%;

  -webkit-animation: base-background 120s ease infinite;
  -moz-animation: base-background 120s ease infinite;
  animation: base-background 120s ease infinite;
}

@-webkit-keyframes base-background {
  0% {
    background-position: 0% 50%
  }

  50% {
    background-position: 100% 50%
  }

  100% {
    background-position: 0% 50%
  }
}

@-moz-keyframes base-background {
  0% {
    background-position: 0% 50%
  }

  50% {
    background-position: 100% 50%
  }

  100% {
    background-position: 0% 50%
  }
}

@keyframes base-background {
  0% {
    background-position: 0% 50%
  }

  50% {
    background-position: 100% 50%
  }

  100% {
    background-position: 0% 50%
  }
}

.title {
  font-weight: bolder;
  color: rgb(0, 0, 0);
}

.main-body {
  margin-bottom: 5%;
}

.subject-body {
  margin-left: auto;
  margin-right: auto;
  background: rgb(165, 239, 246);
  width: 95%;
  flex: auto;
}

.subject-title {
  font-weight: bold;
  overflow: auto;
}

.wrap {
  display: flex;
  flex-wrap: wrap;
  margin-left: 5%;
  margin-right: 5%;
}

.subject-add {
  width: 60%;
  margin-left: auto;
  margin-right: auto;
  background: rgb(165, 239, 246);
  padding: 10px;
}

.title-center {
  display: block;
  margin-left: auto;
  margin-right: auto;
  text-align: center;
}
</style>
