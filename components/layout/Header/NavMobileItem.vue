<template>
  <template v-if="item.links">
    <UiCollapsible v-model:open="isOpen">
      <UiCollapsibleTrigger class="w-full p-2 text-left">
        <div class="flex w-full gap-1">
          {{ item.title }}
          <Icon
            :name="isOpen ? 'lucide:chevrons-down-up' : 'lucide:chevrons-up-down'"
            size="12"
            class="ml-auto self-center"
          />
        </div>
      </UiCollapsibleTrigger>
      <UiCollapsibleContent>
        <ul class="pl-2">
          <li v-for="link in item.links" :key="link.title">
            <component
              :is="link.to ? NuxtLink : 'div'"
              :to="link.to || undefined"
              :target="link.target || undefined"
              class="mb-1 flex w-full gap-2 rounded-md px-3 py-2 transition-all"
              :class="[link.to ? 'hover:bg-muted' : 'cursor-default opacity-90']"
            >
              <SmartIcon v-if="link.icon" :name="link.icon" :size="16" class="mt-1 min-w-5" />

              <div>
                <div class="flex items-center gap-1.5 font-semibold">
                  {{ link.title }}
                  <UiBadge
                    v-if="link.badge?.value"
                    variant="outline"
                    class="h-5 shrink-0 whitespace-nowrap rounded-full border-emerald-500/30 bg-emerald-500/15 px-1.5 text-[10px] font-medium leading-none text-emerald-700 dark:border-emerald-400/30 dark:bg-emerald-400/15 dark:text-emerald-300"
                  >
                    {{ link.badge.value }}
                  </UiBadge>
                </div>
                <div class="text-sm text-muted-foreground">
                  {{ link.description }}
                </div>
              </div>
            </component>
          </li>
        </ul>
      </UiCollapsibleContent>
    </UiCollapsible>
  </template>
  <NuxtLink v-else :to="item.to" :target="item.target" class="flex w-full p-2">
    {{ item.title }}
    <Icon v-if="item.showLinkIcon ?? true" name="lucide:arrow-up-right" class="ml-1 text-muted-foreground" size="12" />
  </NuxtLink>
</template>

<script setup lang="ts">
const props = defineProps<{
  item: any;
  index: number;
}>();

const collapsed = useCollapsedMap();
const isOpen = ref(collapsed.value.get(`mobile-header-nav${props.index}`) || false);
watch(isOpen, (v) => {
  collapsed.value.set(`mobile-header-nav${props.index}`, v);
});
</script>
