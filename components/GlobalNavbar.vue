<template>
  <header class="app-header font-bold" :style="{ background: theme.background, color: theme.color }">
    <div class="inner container">
      <div class="start">
        <div class="box ">
          <nuxt-link class="btn-setting" to="/">
            <font-awesome-icon class="" :icon="['fas', 'home']" />
          </nuxt-link>
        </div>
        <span v-if="menu" class="flex">
          <div v-for="(item, index) in menu" :key="index" class="square">
            <button class="focus:outline-none" @click="$emit(item.action)">{{item.title}}</button>
          </div>
        </span>
      </div>
    </div>
  </header>
</template>

<script lang="ts">
import { computed, defineComponent, ref, useContext } from '@nuxtjs/composition-api'
export default defineComponent({
  name: 'Navbar',
  props: {
    theme: {
      type: Object,
      required: true,
    },
    menu: {
      type: Array,
      required: false,
    },
  },
  setup(props, { emit }) {
    const { store, route, app } = useContext()
    return {
      cekData,
      cek
    }

    function cek(){
      console.log('props', props.menu)
    }
    
    function cekData() {
    }
  },
})
</script>

<style lang="postcss" scoped>

.square {
  @apply rounded-xl flex justify-center px-4 ml-4;
  /* padding: 8px; */
  font-size: 18px;
  place-items: center;
  text-align: center;
  height: 45px;
}
.box {
  @apply rounded-full flex justify-center;
  /* padding: 8px; */
  font-size: 18px;
  place-items: center;
  text-align: center;
  width: 45px;
  height: 45px;
}

.btn-setting {
  width: 25px;
  height: 25px;
}

.app-header {
  @apply fixed w-full top-0 py-4;
  @apply z-30 select-none;
  height: var(--header-height);
  min-width: 320px;
  .inner {
    @apply h-full text-xl;
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