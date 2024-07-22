<template>
  <div class="index-page">
    <a-input-search
      v-model:value="searchText"
      placeholder="input search text"
      enter-button="Search"
      size="large"
      @search="onSearch"
    />
  </div>
  <MyDivide />
  <a-tabs v-model:activeKey="activeKey" @change="onTabChange">
    <a-tab-pane key="post" tab="文章">
      <PostList :postList="postList" />
      <!-- 这里写成 post-list = "postList"也可以-->
    </a-tab-pane>
    <a-tab-pane key="picture" tab="图片">
      <PictureList :picture-list="pictureList" />
    </a-tab-pane>
    <a-tab-pane key="user" tab="用户">
      <UserList :user-list="userList" />
    </a-tab-pane>
    <a-tab-pane key="video" tab="视频">
      <VideoList :video-list="videoList" />
    </a-tab-pane>
  </a-tabs>
</template>

<!--setup 开启 vue3 语法-->
<script setup lang="ts">
import { ref, watchEffect } from "vue";
import PostList from "@/components/PostList.vue";
import UserList from "@/components/UserList.vue";
import PictureList from "@/components/PictureList.vue";
import VideoList from "@/components/VideoList.vue";
import MyDivide from "@/components/MyDivide.vue";
import { useRoute, useRouter } from "vue-router";
import myAxios from "@/plugins/myAxios";
import { message } from "ant-design-vue";

const postList = ref([]);
const pictureList = ref([]);
const userList = ref([]);
const videoList = ref([]);

// 改变 URL 地址
const router = useRouter();
const route = useRoute();
// 当前激活的是哪个标签栏
const activeKey = route.params.category;

const initSearchParams = {
  type: activeKey,
  text: "",
  pageSize: 10,
  pageNum: 1,
};

const searchText = ref(route.query.text);
// 定义变量接收搜索参数
const searchParams = ref(initSearchParams);

/**
 * 加载数据
 */
const loadDataOld = (params: any) => {
  const postQuery = {
    ...params,
    searchText: params.text,
  };

  myAxios.post("post/list/page/vo", postQuery).then((res: any) => {
    postList.value = res.records;
  });

  const pictureQuery = {
    ...params,
    searchText: params.text,
  };

  myAxios.post("picture/list/page/vo", pictureQuery).then((res: any) => {
    pictureList.value = res.records;
  });

  const userQuery = {
    ...params,
    userName: params.text,
  };

  myAxios.post("user/list/page/vo", userQuery).then((res: any) => {
    userList.value = res.records;
  });
};

/**
 * 加载所有数据
 * @param params
 */
const loadAllData = (params: any) => {
  const query = {
    ...params,
    searchText: params.text,
  };

  myAxios.post("search/all", query).then((res: any) => {
    postList.value = res.postList;
    pictureList.value = res.pictureList;
    userList.value = res.userList;
    videoList.value = res.videoList;
  });
};

/**
 * 根据查询类型加载数据
 * @param params
 */
const loadData = (params: any) => {
  const { type } = params;
  if (!type) {
    message.error("类别为空");
    return;
  }
  const query = {
    ...params,
    searchText: params.text,
  };

  myAxios.post("search/all", query).then((res: any) => {
    if (type === "post") {
      postList.value = res.dataList;
    } else if (type === "picture") {
      pictureList.value = res.dataList;
    } else if (type === "user") {
      userList.value = res.dataList;
    } else if (type === "video") {
      videoList.value = res.dataList;
    }
  });
};

/**
 * 核心逻辑: 只要路由变化，就触发 loadData
 */
watchEffect(() => {
  searchParams.value = {
    ...searchParams.value,
    text: route.query.text,
    type: route.params.category,
  } as any;
  loadData(searchParams.value);
});

// 搜索框输入内容后, 会同步到 url, 路由会变化, 路由变化会被监听, 触发loadData
const onSearch = (value: string) => {
  // 在搜索框输入的搜索条件会反馈到 URL 地址
  router.push({
    query: {
      ...searchParams.value,
      text: value,
    },
  });
};

const onTabChange = (key: string) => {
  router.push({
    path: `/${key}`,
    query: {
      ...searchParams.value,
      type: key,
    },
  });
};
</script>
