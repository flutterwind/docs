<template>
  <NavigationMenuItem v-bind="props">
    <slot />
  </NavigationMenuItem>
</template>

<script setup lang="ts">
import type { NavigationMenuItemProps } from 'reka-ui';
import { NavigationMenuItem } from 'reka-ui';

const props = defineProps<NavigationMenuItemProps>();
</script>
