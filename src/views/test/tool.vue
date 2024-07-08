<script setup>
import { ref } from 'vue';
const handleDebounceBtn = () => {
  console.log('防抖');
};
const handleThrottleBtn = () => {
  console.log('节流');
};
const text = ref('这是要复制的内容');

// 弹窗
const dialogRef = ref();

const openDialog = () => {
  dialogRef.value.handleOpen();
};

const closeDialog = () => {
  dialogRef.value.handleClose();
};

const handleConfirm = () => {
  console.log('Confirmed');
};

const handleCancel = () => {
  console.log('Cancelled');
};
</script>

<template>
  <div>
    <el-button type="primary" plain @click="openDialog">打开弹窗</el-button>
    <NovaDialog
        ref="dialogRef"
        :title="'自定义标题'"
        :height="400"
        :width="700"
        :confirmText="'确定'"
        :cancelText="'取消'"
        :destroyOnClose="true"
        :fullscreen="false"
        :loading="false"
        :footerHidden="false"
        @confirm="handleConfirm"
        @cancel="handleCancel"
    >
      <template #content>
        <div>
          <p>这里是自定义内容。</p>
        </div>
      </template>
    </NovaDialog>
    <el-button type="primary" plain v-debounce:500="handleDebounceBtn">按钮防抖指令</el-button>
    <el-button type="primary" plain v-throttle:10000="handleThrottleBtn">按钮节流指令</el-button>
    <el-button type="primary" plain v-copy="text" class="">点我复制</el-button>
    {{ text }}
    <div class="text-5xl text-center mt-2 animate__animated animate__tada">测试动画</div>
  </div>
</template>

<style scoped lang="scss"></style>
