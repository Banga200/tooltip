<template>
  <div class="tooltip-wrapper" ref="wrapper">
    <div 
      ref="content" 
      class="text-content"
      @mouseenter="checkOverflow"
      @mouseleave="showTooltip = false"
    >
      <slot></slot>
    </div>
    <div 
      v-if="showTooltip" 
      class="tooltip"
      :style="{ top: tooltipPosition.top + 'px', left: tooltipPosition.left + 'px' }"
    >
      <slot></slot>
    </div>
  </div>
</template>

<script setup>
const wrapper = ref(null)
const content = ref(null)
const showTooltip = ref(false)
const tooltipPosition = ref({ top: 0, left: 0 })

const checkOverflow = () => {
  if (content.value) {
    console.log(content.value.scrollWidth , content.value.clientWidth)
    const isOverflowing = content.value.scrollWidth > content.value.clientWidth
    showTooltip.value = isOverflowing
    
    if (isOverflowing) {
      const rect = content.value.getBoundingClientRect()
      tooltipPosition.value = {
        top: -30, // Show tooltip above the text
        left: 0
      }
    }
  }
}
</script>

<style scoped>
.tooltip-wrapper {
  position: relative;
  width: 100%;
}

.text-content {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width: 100%;
}

.tooltip {
  position: absolute;
  background-color: #333;
  color: white;
  padding: 5px 10px;
  border-radius: 4px;
  font-size: 14px;
  white-space: nowrap;
  z-index: 1000;
  pointer-events: none;
}

.tooltip::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 50%;
  transform: translateX(-50%);
  border-width: 5px;
  border-style: solid;
  border-color: #333 transparent transparent transparent;
}
</style>