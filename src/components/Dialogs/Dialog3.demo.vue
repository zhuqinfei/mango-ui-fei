<demo>
支持 title
</demo>
<template>
<div>
  <Button theme="primary" @click="toggle">打开对话框带标签</Button>
  <Dialog v-model:visible="visible" title="自定义标签">
    <p>这是内容</p>
  </Dialog>
</div>
</template>

<script lang="ts">
import Dialog from '../../lib/Dialog.vue'
import Button from '../../lib/Button.vue'
import {ref} from 'vue'
export default {
  components: {Dialog,Button},
  setup() {
    const visible = ref(false)
    const toggle = () => {visible.value = !visible.value}
    return {visible,toggle}
  }
}
</script>