<script lang="ts" setup>
import { appKeywords } from "@/constants/index";

useSeoMeta({
  title: "极物圈登录",
  description: "极物 - 聊天 - 极物圈 开启你的极物之旅！",
  keywords: appKeywords,
});
const user = useUserStore();
definePageMeta({
  key: route => route.fullPath,
  layout: false,
});

const [autoAnimateRef, enable] = useAutoAnimate({});
onMounted(() => {
  const setting = useSettingStore();
  enable(!setting.settingPage.isColseAllTransition);
});
</script>

<template>
  <div
    v-if="user.showLoginForm || user.showRegisterForm"
    class="relative min-h-100vh flex-1 overflow-hidden overflow-hidden shadow border-default card-default bg-color"
    grid="~ cols-1 md:cols-2"
  >
    <div fixed right-4 top-4 flex items-center gap-2>
      <MenuController key="header" :show-max="false" />
    </div>
    <!-- bg -->
    <div hidden h-full w-full border-0 border-r-1px shadow-md shadow-inset md:block border-default>
      <ElImage data-tauri-drag-region src="/images/login_bg.jpg" fit="cover" class="h-full select-none overflow-hidden rounded-r-0 card-default" />
    </div>
    <!-- 表单 -->
    <div class="flex flex-col select-none pt-20vh">
      <div ref="autoAnimateRef" mx-a class="w-5/6 text-center sm:(w-3/5 text-left)">
        <div key="login-bg" class="fixed left-4 top-0 flex items-center gap-2 py-4 sm:(relative left-a top-a)">
          <ElImage
            data-tauri-drag-region
            src="/logo.png" class="h-2em w-2em"
          />
          <strong data-tauri-drag-region class="font-bold tracking-0.2em op-80">
            极物聊天 | JIWU
          </strong>
        </div>
        <!-- 登录 -->
        <FormLoginForm
          v-if="user.showLoginForm"
          key="login-form"
          data-tauri-drag-region
        />
        <!-- 注册 -->
        <FormRegisterForm
          v-else-if="user.showRegisterForm"
          key="register-form"
          data-tauri-drag-region
        />
      </div>
    </div>
  </div>
</template>
