<template>
  <div id="app">
    <header>
      <router-link to="/"><img alt="Doggy" src="./assets/dog.png"></router-link>
    </header>
    <nav>
      <button><router-link to="/stream/new">New</router-link></button>
      <button @click="askStreamName = true">Join</button>
    </nav>

    <router-view />

    <dialog open v-show="askStreamName">
      <button @click="askStreamName = false" class="close-btn">&times;</button>
      <form @submit.prevent="joinStream">
        <label>Stream name:
          <input type="text" v-model="streamName">
        </label>

        <button type="submit">Join</button>
      </form>
    </dialog>

    <footer>
      <a href="https://andreasvirkus.me">author</a> |
      <a href="https://github.com/andreasvirkus/pupper">code</a>
    </footer>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      askStreamName: false,
      streamName: ''
    }
  },
  methods: {
    joinStream () {
      this.$router.push(`/stream/${this.streamName}`)
    }
  }
}
</script>

<style lang="scss">
/* Handicraft reset */
*,
*::before,
*::after {
  box-sizing: inherit;
}
html {
  box-sizing: border-box;
}
body {
  min-height: 100vh;
  margin: 0;
  padding: 0;
}
body,
button,
input,
textarea {
  font-family: -apple-system, system-ui, BlinkMacSystemFont, "Segoe UI", Roboto, Ubuntu;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#app {
  display: flex;
  flex-direction: column;
  text-align: center;
  color: #2c3e50;
  height: 100vh;
}

nav {
  padding: 2rem;

  a {
    color: #2c3e50;
    text-decoration: none;
  }
}

button {
  border: 2px solid #222;
  background: none;
  padding: .4rem .75rem;
  font-size: 1rem;
  cursor: pointer;
}
button + button {
  margin-left: 1rem;
}
section {
  flex: 1;
  margin: 2rem auto;
}
footer {
  padding: 3rem;
}

dialog {
  top: 40vh;
  padding: 2rem;

  &::before {
    content: '';
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: -1;
    background: rgba(0,0,0,.25);
  }
}
form {
  display: flex;
  flex-direction: column;

  button {
    margin-top: 1rem;
  }
}
.close-btn {
  position: absolute;
  top: 0;
  right: 0;
  border: none;
}
</style>
