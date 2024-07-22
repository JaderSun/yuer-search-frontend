<script setup lang="ts">
import { withDefaults, defineProps } from "vue";

interface Props {
  pictureList: any[];
}

const props = withDefaults(defineProps<Props>(), {
  pictureList: () => [],
});
</script>

<template>
  <a-list
    item-layout="horizontal"
    :grid="{ gutter: 10, xs: 1, sm: 2, md: 4, lg: 4, xl: 6, xxl: 3 }"
    :data-source="props.pictureList"
  >
    <template #renderItem="{ item }">
      <a-list-item>
        <a :href="item.url">
          <a-card hoverable>
            <template #cover>
              <img alt="example" :src="item.url" class="fixed-height-image" />
            </template>
            <a-card-meta :title="item.title"></a-card-meta>
          </a-card>
        </a>
      </a-list-item>
    </template>
  </a-list>
</template>

<style scoped>
.fixed-height-image {
  height: 300px; /* 固定高度 */
  width: 100%; /* 宽度自动调整 */
  object-fit: cover; /* 保持图片比例，并裁剪以适应 */
}
</style>
