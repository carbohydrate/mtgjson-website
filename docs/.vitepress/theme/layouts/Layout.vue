<template lang="pug">
Layout
  template(#sidebar-nav-before)
    Searchbar
  template(#not-found)
    NotFound
</template>

<script setup lang="ts">
import { onMounted } from 'vue';
import DefaultTheme from 'vitepress/theme';
import Searchbar from '../components/Searchbar.vue';
import NotFound from '../components/NotFound.vue';
import { useStore } from '../store';

const { Layout } = DefaultTheme;

const store = useStore();
const storeValues: string[] = ['Meta', 'EnumValues', 'SetList', 'DeckList']

onMounted(async (): Promise<void> => {
  storeValues.forEach(async ( value: string ): Promise<void> => {
    if ( Object.keys(store[value] ).length === 0) {
      await store.fetchJSON(value);
    }
  });
});
</script>
