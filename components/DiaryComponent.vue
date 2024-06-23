<template>
  <div class="diary">
    <pre
      ref="preElement"
      contenteditable="true"
      class="content"
      @input="onInput"
    ></pre>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const preElement = ref(null)
const key = 'pre'

const onInput = () => {
  const content = preElement.value.innerText
  // console.log('===2', content)
  localStorage.setItem(key, content)
}

onMounted(() => {
  const content = localStorage.getItem(key)
  if (!content || !preElement.value) return

  // console.log('===1', content, preElement.value)
  preElement.value.innerText = content
})
</script>

<style scoped>
.content {
  white-space: pre-wrap; /* CSS3 */
  word-wrap: break-word; /* IE */
  line-height: 2em;
  font-size: 20px;
  position: relative;
  width: 100%;
  outline: none;
}

.content::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: repeating-linear-gradient(
    to bottom,
    transparent 0,
    transparent calc(2.1em - 3px),
    black calc(2.1em - 2px)
  );
  pointer-events: none;
}
</style>
