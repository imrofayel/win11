<template>
  <div class="flex justify-between w-full h-12 backdrop-blur-lg bg-white/85 dark:bg-black/70">
    <div class="flex p-3 space-x-5">

      <img 
        ref="startButton"
        src="/assets/Taskbar/Start_Light.png" 
        class="icon pl-2 transform hover:scale-110 duration-500 ease-in-out"
        @click="handleClick('startButton')"
        :class="{ 'clicked': clickedButton === 'startButton' }"
      />

      <img 
        ref="taskViewButton"
        src="/assets/Taskbar/TaskView_Light.png" 
        class="icon pl-1 transform hover:scale-110 duration-500 ease-in-out"
        @click="handleClick('taskViewButton')"
        :class="{ 'clicked': clickedButton === 'taskViewButton' }"
      />

      <img 
        ref="edgeButton"
        src="/assets/Taskbar/Edge_256.png" 
        class="icon transform hover:scale-110 duration-500 ease-in-out"
        @click="handleClick('edgeButton')"
        :class="{ 'clicked': clickedButton === 'edgeButton' }"
      />

      <img 
        ref="explorerButton"
        src="/assets/Taskbar/Explorer_256.png" 
        class="icon transform hover:scale-110 duration-500 ease-in-out"
        @click="handleClick('explorerButton')"
        :class="{ 'clicked': clickedButton === 'explorerButton' }"
      />

      <img 
        ref="storeButton"
        src="/assets/Taskbar/Store_256.png" 
        class="icon transform hover:scale-110 duration-500 ease-in-out"
        @click="handleClick('storeButton')"
        :class="{ 'clicked': clickedButton === 'storeButton' }"
      />

    </div>

    <div class="px-3 flex space-x-1 text-gray-900/90">
      
      <div class="space-x-3 hover:bg-white/30 p-2 m-1 rounded-lg hover:border border-gray/10 relative mr-0 hover:scale-[1.04] duration-500 ease-in-out transform"><Icon name="fluent:wifi-1-24-regular" size="21px"></Icon>

      <Icon name="fluent:speaker-2-32-regular" size="20px"></Icon>
      <Icon name="fluent:battery-4-28-regular" size="21px"></Icon></div>

      <Icon name="fluent:alert-32-regular" size="23px" class="relative top-3 pr-8 transform hover:scale-110 duration-500 ease-in-out"></Icon>

      <img 
        ref="copilotButton"
        src="/assets/Icons/Microsoft_365_Copilot_Icon.svg" 
        class="icon transform hover:scale-95 duration-500 ease-in-out py-2 pl-2 scale-[.8]"
        @click="handleClick('storeButton')"
        :class="{ 'clicked': clickedButton === 'storeButton' }"
      />

    </div>

  </div>
</template>

<script lang="ts" setup>

const clickedButton = ref('');

const handleClick = (buttonRef: string) => {
  clickedButton.value = buttonRef;
  setTimeout(() => {
    clickedButton.value = '';
  }, 240); // 300ms hold time
};

</script>

<style scoped>
.icon {
  transition: transform 500ms ease-in, transform 500ms ease-out;
}

.icon.clicked {
  transform: scale(0.8);
}
</style>
