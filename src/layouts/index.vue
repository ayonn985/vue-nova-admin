<script setup>
import { useScreenStore } from '@/hooks/screen/index.js';
import { computed } from 'vue';
// 全局主题配置
import useGlobalStore from '@/stores/modules/global.js';
import ThemeConfig from '@/layouts/components/ThemeConfig/index.vue';
import LayoutVertical from '@/layouts/LayoutVertical/index.vue';
import LayoutColumns from '@/layouts/LayoutColumns/index.vue';
import LayoutClassic from '@/layouts/LayoutClassic/index.vue';
import LayoutHorizontal from '@/layouts/LayoutHorizontal/index.vue';
import LayoutMobile from '@/layouts/LayoutMobile/index.vue';

// type LayoutType = "vertical" | "columns" | "classic" | "horizontal" | string;
const LayoutComponent = {
  vertical: LayoutVertical,
  columns: LayoutColumns,
  classic: LayoutClassic,
  horizontal: LayoutHorizontal
};

// 全局主题仓库
const globalStore = useGlobalStore();
// 获取布局格式
const layout = computed(() => globalStore.layout);
// 获取当前为[移动端、IPad、PC端]仓库，阔以使用 watchEffect(() => {}) 进行监听。
const { isMobile } = useScreenStore();
</script>

<template>
  <!-- 同级进行选择不同布局时就不会被关闭 -->
  <ThemeConfig />
  <component :is="LayoutComponent[layout]" v-if="!isMobile" />
  <component :is="LayoutMobile" v-if="isMobile" />
</template>

<style scoped></style>
