<template>
    <nav class="flex-1 space-y-1 bg-slate-800 px-2" aria-label="Sidebar">
      <template v-for="item in props.navigation" :key="item.name">
        <div v-if="!item.children">
          <a
            v-if="!item.name.startsWith('Search')"
            :href="item.href">
            {{ item.name }}
          </a>
        </div>
        <Disclosure v-else v-slot="{ open }" as="div" class="space-y-1" :default-open="item.children.map((x) => x.href).includes(props.page)">
          <DisclosureButton>
            {{ item.name }}
          </DisclosureButton>
          <DisclosurePanel class="space-y-1">
            <DisclosureButton
              v-for="subItem in item.children"
              :key="subItem.name"
              as="a"
              :href="subItem.href"
              :target="[subItem.isExternal === true ? '_blank' : '']"
              :rel="subItem.isExternal === true ? 'nofollow noopener' : ''"
              class="group flex w-full items-center rounded-md py-2 pl-10 pr-2 text-sm font-medium hover:bg-slate-50 hover:text-slate-900">
              {{ subItem.name }}
            </DisclosureButton>
          </DisclosurePanel>
        </Disclosure>
      </template>
      <div class="h-4 bg-slate-800"></div>
    </nav>
    
</template>

<script setup lang="ts">
import { Disclosure, DisclosureButton, DisclosurePanel } from '@headlessui/vue';

import type { PropType } from 'vue';

interface NavigationItem {
  name: string;
  href: string;
  children: NavigationChild[];
}

interface NavigationChild {
  name: string;
  href: string;
  isExternal: boolean;
}

const props = defineProps({
  navigation: {
    type: Array as PropType<Array<NavigationItem>>,
    required: true,
  },
});
</script>