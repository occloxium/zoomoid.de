<template>
  <main id="app">
    <router-view class="view bg-zoomoid-gradient" v-slot="{ Component }">
      <transition :name="transitionName" mode="out-in">
        <component :is="Component"></component>
      </transition>
    </router-view>
    <Footer></Footer>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import Footer from "./components/Footer.vue";

export default defineComponent({
  name: "App",
  components: {
    Footer,
  },
  data: () => ({
    transitionName: "slide-right",
  }),
  watch: {
    $route(to, from) {
      const toDepth = to.path
        .split("/")
        .filter((s: string) => s.length !== 0).length;
      const fromDepth = from.path
        .split("/")
        .filter((s: string) => s.length !== 0).length;
      this.transitionName = toDepth < fromDepth ? "slide-right" : "slide-left";
    },
  },
});
</script>

<style lang="postcss">
.slide-left-enter,
.slide-right-leave-active {
  opacity: 0;
  transform: translate(50vw, 0);
}
.slide-left-leave-active,
.slide-right-enter {
  opacity: 0;
  transform: translate(-50vw, 0);
}
.view {
  transition: all 0.2s cubic-bezier(0.55, 0, 0.1, 1);
  @apply flex flex-col flex-grow;
  @apply text-white;
}
#app {
  @apply min-h-screen flex flex-col;
  overflow: hidden;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
