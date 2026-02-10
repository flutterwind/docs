<template>
  <UiNavigationMenu>
    <UiNavigationMenuList>
      <UiNavigationMenuItem v-for="(item, i) in nav" :key="i" class="relative">
        <template v-if="item.links">
          <UiNavigationMenuTrigger class="bg-transparent font-semibold">
            {{ item.title }}
          </UiNavigationMenuTrigger>
          <UiNavigationMenuContent>
            <ul class="w-[250px] p-2">
              <li v-for="link in item.links" :key="link.title">
                <UiNavigationMenuLink v-if="link.to" as-child>
                  <NuxtLink
                    :to="link.to"
                    :target="link.target || undefined"
                    class="mb-1 flex w-full gap-2 rounded-md px-3 py-2 transition-all hover:bg-muted"
                  >
                    <SmartIcon v-if="link?.icon" :name="link.icon" :size="16" class="mt-1 min-w-5" />

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
                  </NuxtLink>
                </UiNavigationMenuLink>

                <div
                  v-else
                  class="mb-1 flex w-full cursor-default gap-2 rounded-md px-3 py-2 opacity-90"
                >
                  <SmartIcon v-if="link?.icon" :name="link.icon" :size="16" class="mt-1 min-w-5" />

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
                </div>
              </li>
            </ul>
          </UiNavigationMenuContent>
        </template>
        <NuxtLink v-else :to="item.to" :target="item.target">
          <Icon v-if="item.showLinkIcon ?? true" name="lucide:arrow-up-right" class="absolute right-2 top-2 text-muted-foreground" size="13" />
          <div class="bg-transparent font-semibold" :class="[navigationMenuTriggerStyle(), (item.showLinkIcon ?? true) && 'pr-6']">
            {{ item.title }}
          </div>
        </NuxtLink>
      </UiNavigationMenuItem>
    </UiNavigationMenuList>
  </UiNavigationMenu>
</template>

<script setup lang="ts">
import { navigationMenuTriggerStyle } from '@/components/ui/navigation-menu';

const { nav } = useConfig().value.header;
</script>
