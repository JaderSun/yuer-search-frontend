<script setup lang="ts">
import { withDefaults, defineProps } from "vue";

interface Props {
  videoList: any[];
}

const props = withDefaults(defineProps<Props>(), {
  videoList: () => [],
});
</script>

<template>
  <a-list
    item-layout="horizontal"
    :grid="{ gutter: 16, xs: 1, sm: 2, md: 4, lg: 4, xl: 6, xxl: 3 }"
    :data-source="props.videoList"
  >
    <template #renderItem="{ item }">
      <a-list-item>
        <a :href="item.url">
          <a-card hoverable>
            <template #cover>
              <img :src="item.pic" referrerpolicy="no-referrer" />
            </template>
            <a :href="item.url">
              <a-card-meta :title="item.title" />
            </a>
          </a-card>
        </a>
      </a-list-item>
    </template>
  </a-list>
</template>

<style scoped>
.fixed-height-image {
  height: 200px;
  width: 100%;
  object-fit: cover;
}
</style>
