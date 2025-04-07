<template>
  <div>
    <div class="sidebar" style="width: 240px;">
      <ul>
        <li v-for="item in items" :key="item">
          <TooltipText>{{ item }}</TooltipText>
        </li>
      </ul>
    </div>
  </div>
</template>

<script setup>
// Example items with some long text
const items = [
  'Short text',
  'This is a very long text that will definitely overflow the container width and show a tooltip',
  'Another normal text',
  'Yet another very long text that will need to show a tooltip because it exceeds the container width'
]
</script>

<style>
.sidebar {
  background-color: #f5f5f5;
  padding: 1rem;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  padding: 0.5rem;
  border-bottom: 1px solid #ddd;
}
</style>