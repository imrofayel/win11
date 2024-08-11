<script setup lang="ts">
import { useMouse, useWindowScroll } from '@vueuse/core'
import { ref, unref } from 'vue'

const { x, y } = useMouse()
const { y: windowY } = useWindowScroll()

const isOpen = ref(false)
const virtualElement = ref({ getBoundingClientRect: () => ({}) })

function onContextMenu(event: MouseEvent) {
  event.preventDefault();

  const top = unref(y) - unref(windowY)
  const left = unref(x)

  virtualElement.value.getBoundingClientRect = () => ({
    width: 0,
    height: 0,
    top,
    left
  })

  isOpen.value = true
}

function handleMenuClick() {
  isOpen.value = false;
}

</script>

<template>
  <div class="w-full h-[548px]" @contextmenu="onContextMenu">

    <div class="select-none w-full h-full flex items-center justify-center">

    </div>

    <!-- Context Menu -->
    <UContextMenu v-model="isOpen" :virtual-element="virtualElement" :ui="{
      background: 'backdrop-blur-lg bg-white/85 dark:bg-gray-900',
      shadow: 'shadow-none',
      ring: '',
      rounded: 'rounded-xl',

      transition: {
        enterActiveClass: 'transition ease-in duration-200',
      },

    }">

      <div class="scale-[0.88]"><div class="min-w-[220px] text-[#263238ee]">

        <!--View-->
        <div class="flex items-center mt-1 py-2 px-2 pr-[11px] hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick">

          <div><Icon name="fluent:border-right-20-filled" size="24px" class="mr-2 opacity-90"/>

          <span class="pl-1 relative -top-[6px] text-[18px] opacity-90">View</span></div>

          <Icon name="fluent:chevron-right-20-filled" size="22px" class="relative -top-[2px] opacity-90"></Icon>

        </div>  

        <!--Sort-->
        <div class="flex items-center py-2 px-2 pr-[11px] hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick">

          <div><Icon name="fluent:align-stretch-horizontal-16-regular" size="24px" class="mr-2 opacity-90"/>

          <span class="pl-1 relative -top-[6px] text-[18px] opacity-90">Sort by</span></div>

          <Icon name="fluent:chevron-right-20-filled" size="22px" class="relative -top-[2px] opacity-90"></Icon>

        </div>  

        <!--Refresh-->
        <div class="flex items-center py-2 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick">

          <div><Icon name="fluent:arrow-counterclockwise-20-filled" size="24px" class="mr-2 opacity-90"/>

          <span class="pl-1 relative -top-[6px] text-[18px] opacity-90">Refresh</span></div>

        </div>  

        <!--Display-->
        <div class="flex items-center py-2 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick">

          <div><Icon name="fluent:person-16-regular" size="29px" class="mr-2 opacity-90"/>

          <span class="relative -top-[8px] text-[18px] opacity-90">Settings</span></div>

        </div>  

      <!--Options-->
      <div class="flex justify-between items-center py-2 pt-[10px] px-1">

        <div class="flex items-center py-1 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick"><Icon name="fluent:arrow-exit-20-filled" size="24px"></Icon></div>

        <div class="flex items-center py-1 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick"><Icon name="fluent:add-circle-16-regular" size="27px"></Icon></div>

        <div class="flex items-center py-1 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick"><Icon name="fluent:clipboard-multiple-16-regular" size="25px"></Icon></div>

        <div class="flex items-center py-1 px-2 hover:bg-white/50 dark:hover:bg-gray-700 rounded-xl cursor-pointer justify-between hover:scale-105 duration-500 transition ease-in-out" @click="handleMenuClick"><Icon name="fluent:arrow-undo-32-filled" size="23px"></Icon></div>

        </div> 

      </div></div>
      
    </UContextMenu>

  </div>
</template>

<style scoped>
/* Custom styling to give it a Windows 11 look */
.placeholder {
  background-color: #ffffff;
  color: #000000;
  border-radius: 8px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.u-context-menu {
  border-radius: 8px;
  box-shadow: 0 4px 14px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(12px);
  background-color: rgba(255, 255, 255, 0.75);
}

.dark .u-context-menu {
  background-color: rgba(32, 32, 32, 0.85);
}

.dark .placeholder {
  background-color: #1e1e1e;
  color: #ffffff;
}
</style>
