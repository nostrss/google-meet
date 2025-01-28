<template>
  <div>This is the Add-on Main Stage. Everyone in the call can see this.</div>
  <div>Hello, world!</div>
</template>

<script lang="ts" setup>
import { onMounted } from "vue";
import { meet } from "@googleworkspace/meet-addons/meet.addons";

/**
 * 컴포넌트가 마운트될 때 Add-on Main Stage Client를 초기화합니다.
 */
onMounted(async () => {
  try {
    const session = await meet.addon.createAddonSession({
      cloudProjectNumber: import.meta.env.VITE_GOOGLE_PROJECT_NUMBER, // 실제 프로젝트 번호로 교체하세요.
    });
    await session.createMainStageClient();
    console.log("Main Stage Client initialized successfully.");
  } catch (error) {
    console.error("Failed to initialize Main Stage Client:", error);
  }
});
</script>

<style scoped>
/* 필요에 따라 스타일을 추가하세요 */
div {
  margin-bottom: 10px;
  font-size: 18px;
}

div:last-child {
  font-weight: bold;
}
</style>
