<script setup lang="ts">
import { RouterLink } from 'vue-router';
import { Icon } from '@iconify/vue';
import { theme } from '@/shared/data/theme';
import { useTermStore } from '@/shared/stores/term';

const store = useTermStore();
</script>

<template>
  <header class="sticky z-30 w-full shadow navbar bg-base-100">
    <nav class="container flex justify-between mx-auto">
      <RouterLink to="/" class="text-xl btn btn-ghost text-base-content">
        Slangio <span class="badge badge-outline">BETA</span>
      </RouterLink>
      <ul class="menu menu-xs sm:menu-md menu-horizontal">
        <li>
          <RouterLink to="/collections" class="tooltip tooltip-bottom" data-tip="Collections">
            <Icon icon="heroicons:book-open-solid" class="text-lg sm:text-xl" />
          </RouterLink>
        </li>
        <li>
          <RouterLink to="/quiz" class="relative tooltip tooltip-bottom" data-tip="Learn">
            <Icon
              icon="heroicons:academic-cap-solid"
              class="text-lg sm:text-xl"
              :class="store.hasToLearn ? 'chameleon' : ''"
            />
          </RouterLink>
        </li>
        <li>
          <RouterLink to="/settings" class="tooltip tooltip-bottom" data-tip="Settings">
            <Icon icon="heroicons:cog-6-tooth-solid" class="text-lg sm:text-xl" />
          </RouterLink>
        </li>
        <li>
          <button
            @click="theme = theme === 'light' ? 'dark' : 'light'"
            class="tooltip tooltip-bottom"
            :data-tip="theme === 'light' ? 'Light Mode' : 'Dark Mode'"
          >
            <Icon v-if="theme === 'light'" icon="heroicons:sun" class="text-lg sm:text-xl" />
            <Icon v-else icon="heroicons:moon" class="text-lg sm:text-xl" />
          </button>
        </li>
      </ul>
    </nav>
  </header>
</template>

<style>
.chameleon {
  animation: chameleon 3s ease-in-out alternate infinite;
}

@keyframes chameleon {
  0% {
    @apply text-base-content;
  }

  50% {
    @apply text-success;
  }

  100% {
    @apply text-base-content;
  }
}
</style>
