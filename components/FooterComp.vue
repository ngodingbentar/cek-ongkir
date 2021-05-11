<template>
    <div class="py-4" :style="{ background: storeTheme.background, color: storeTheme.color }">
      <div class="text-center">
        <a href="https://www.instagram.com/ngodingbentar/" target="_blank">@ngodingbentar</a>
        /
        <a href="https://www.instagram.com/dewaqintoro/" target="_blank">@dewaqintoro</a>
      </div>
    </div>
</template>

<script lang="ts">
import { computed, defineComponent, ref, useContext } from '@nuxtjs/composition-api'
export default defineComponent({
  name: 'Footer',
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
    }
  },
})
</script>

<style lang="postcss" scoped>

</style>