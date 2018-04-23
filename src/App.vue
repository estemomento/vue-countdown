<template>
  <div id="app">
    <countdown year="2018" month="12" day="10" hour="17" minute="30" second="0" />
  </div>
</template>

<script>
import Countdown from './components/countdown'

export default {
  components: { Countdown }
}
</script>

<style lang="scss">
* {
  margin: 0;
  padding: 0;
  user-select: none;
}

#app {
  width: 100vw;
  height: 100vh;
  font-family:-apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  display: flex;
  align-items: center;
  justify-content: center;
}

</style>
