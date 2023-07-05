<template>
  <button type="button" @click="flag = !flag">Toggle</button>

  <Transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello World!</h2>
    <h2 v-else key="secondary">another Hello!</h2>
  </Transition>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: false,
    };
  },
};
</script>

<style>
.fade-enter-from {
  opacity: 0;
}

.fade-enter-active {
  transition: all 0.5s linear;
}

.fade-enter-to{
  transition: all 0.5s linear;
  color: red;
}

.fade-leave-form{
  transition: all 0.5s linear;
  background-color: aquamarine;
}

.fade-enter-active{
  transition: all 0.3s;
  background-color: chartreuse;
}

.fade-leave-to {
  transition: all 3s linear;
  opacity: 0;
}
</style>
