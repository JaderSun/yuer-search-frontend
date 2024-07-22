<script setup lang="ts">
import gg from "../assets/gg.jpg";
import { withDefaults, defineProps } from "vue";

interface Props {
  postList: any[];
}

const props = withDefaults(defineProps<Props>(), {
  postList: () => [],
});
</script>

<!--<template>-->
<!--  <a-list item-layout="horizontal" :data-source="props.postList">-->
<!--    <template #renderItem="{ item }">-->
<!--      <a-list-item>-->
<!--        <a-list-item-meta :description="item.content">-->
<!--          <template #title>-->
<!--            <a href="https://www.antdv.com/">{{ item.title }}</a>-->
<!--          </template>-->
<!--          <template #avatar>-->
<!--            <a-avatar :src="gg" />-->
<!--          </template>-->
<!--        </a-list-item-meta>-->
<!--      </a-list-item>-->
<!--    </template>-->
<!--  </a-list>-->
<!--</template>-->

<template>
  <a-list item-layout="horizontal" :data-source="props.postList">
    <template #renderItem="{ item }">
      <a-list-item>
        <a-list-item-meta>
          <template #title>
            <a href="https://www.antdv.com/">
              <span v-html="item.title"></span>
            </a>
          </template>
          <template #description>
            <a href="https://www.antdv.com/">
              <span class="custom-content" v-html="item.content"></span>
            </a>
          </template>
          <template #avatar>
            <a-avatar :src="gg" />
          </template>
        </a-list-item-meta>
      </a-list-item>
    </template>
  </a-list>
</template>

<style scoped>
.custom-content {
  color: black; /* 你可以根据需要修改颜色 */
}
</style>
