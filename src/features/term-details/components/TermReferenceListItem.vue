<script setup lang="ts">
import { vaultService } from '@/shared/services/vault.service';
import { inject, ref } from 'vue';
import EditTermReference from './EditTermReference.vue';
import { Icon } from '@iconify/vue';
import type { TermReference } from '@/shared/types/term';

defineProps<{ reference: TermReference; index: number }>();

const termId = inject<string>('termId')!;

const editMode = ref(false);
</script>

<template>
  <div v-if="!editMode" class="flex items-center justify-between gap-2">
    <a
      :href="reference.url"
      target="_blank"
      rel="noreferrer nofollow"
      class="link line-clamp-1 w-80"
    >
      {{ reference.name || reference.url }}
    </a>
    <div class="flex items-center gap-1">
      <button
        @click="editMode = true"
        class="btn btn-circle btn-xs tooltip tooltip-bottom"
        data-tip="Edit"
      >
        <Icon icon="heroicons:pencil-16-solid" class="mx-auto" />
      </button>
      <button
        @click="vaultService.removeTermReference(termId, index)"
        class="btn btn-circle btn-xs tooltip tooltip-bottom"
        data-tip="Delete"
      >
        <Icon icon="heroicons:trash-16-solid" class="mx-auto" />
      </button>
    </div>
  </div>
  <EditTermReference v-else :reference :index @close="editMode = false" />
</template>
