<template>
  <header v-if="!loadingTheme" class="app-header font-arabic font-bold" :style="{ background: storeTheme.background, color: storeTheme.color }">
    <div class="inner container">
      <div class="start box" :style="{ boxShadow: storeTheme.boxShadow }">
        <nuxt-link class="btn-setting" to="/agama">
          <font-awesome-icon :icon="['fas', 'home']" />
        </nuxt-link>
      </div>
      <div class="end box" :style="{ boxShadow: storeTheme.boxShadow }">
        <button class="btn-setting focus:outline-none" @click="doSetting()">
          <font-awesome-icon :icon="['fas', 'cog']" />
        </button>
      </div>
      <Transition name="drawer">
        <Setting :theme="storeTheme" v-if="isSetting" @close="closeModal" />
      </Transition>
    </div>
  </header>
</template>

<script lang="ts">
import { computed, defineComponent, ref, useContext } from '@nuxtjs/composition-api'
export default defineComponent({
  name: 'Navbar',
  props: {
    // theme: {
    //   type: Object,
    //   required: true,
    // },
  },
  setup(_, { emit }) {
    const { store, route, app } = useContext()
    const isSetting = ref(false)
    const thisSub = app.$cookies.get('sub')
    const thisAudio = app.$cookies.get('audio')
    const initTheme = computed(() => store.state.initTheme)
    const thisTheme = app.$cookies.get('theme')
    const loadingTheme = computed(() => store.state.loadingTheme)
    const storeTheme = computed(() => store.state.theme)

    if(!thisSub){
      store.dispatch('setSub', 'On')
    } else {
      store.dispatch('getSub')
    }
    if(!thisAudio){
      store.dispatch('setAudio', 'On')
    } else {
      store.dispatch('getAudio')
    }
    if(thisTheme){
      store.dispatch('getTheme')
    } else {
      store.dispatch('setTheme', initTheme.value)
    }

    return {
      storeTheme,
      loadingTheme,
      isSetting,
      cekData,
      closeModal,
      doSetting,
    }
    
    function closeModal() {
      isSetting.value = false
    }
    function doSetting() {
      isSetting.value = true
    }
    function cekData() {
    }
  },
})
</script>

<style lang="postcss" scoped>
.box {
  @apply rounded-full flex justify-center;
  padding: 10px;
  font-size: 20px;
  place-items: center;
  text-align: center;
}

.btn-setting {
  width: 25px;
  height: 25px;
}

@font-face {
  font-family: "lpmq";
  src: url(/fonts/lpmq.otf) format("opentype");
  font-display: swap;
}
.font-arabic{
  font-family: "lpmq", Arial, sans-serif;
  line-height: 2;
}
.app-header {
  @apply fixed w-full top-0 py-4;
  @apply z-30 select-none;
  height: var(--header-height);
  min-width: 320px;
  .inner {
    @apply flex flex-wrap justify-between h-full text-xl;
    @apply px-8;
  }
  .start {
    @apply flex items-center;
  }
  .end {
    /* @apply grid grid-flow-col gap-4; */
  }
  .line {
    @apply block w-px opacity-50 mr-3;
    height: 32px;
  }
}
@screen mobile {
}
@screen sm {
}
@screen md {
  .app-header {
    @apply flex-shrink-0;
    /* @apply relative; */
  }
}
</style>