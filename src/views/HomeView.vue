<script lang="ts" setup>
import { ref, onMounted } from "vue";
import { meet, type MeetSidePanelClient } from "@googleworkspace/meet-addons/meet.addons";

// 상태 변수로 SidePanelClient을 관리합니다.
const sidePanelClient = ref<MeetSidePanelClient | null>(null);

/**
 * 메인 스테이지에서 액티비티를 시작합니다.
 */
const startActivity = async () => {
  if (!sidePanelClient.value) {
    throw new Error("Side Panel is not yet initialized!");
  }
  await sidePanelClient.value.startActivity({
    mainStageUrl: "/main",
  });
};

/**
 * 컴포넌트가 마운트될 때 Add-on Side Panel Client를 초기화합니다.
 */
onMounted(async () => {
  try {
    const session = await meet.addon.createAddonSession({
      cloudProjectNumber: import.meta.env.VITE_GOOGLE_PROJECT_NUMBER,
    });
    sidePanelClient.value = await session.createSidePanelClient();
  } catch (error) {
    console.error("Failed to initialize Side Panel Client:", error);
  }
});
</script>

<template>
  <div>This is the Add-on Side Panel. Only you can see this.</div>
  <button @click="startActivity">Launch Activity in Main Stage.</button>
</template>

<style scoped>
/* 필요에 따라 스타일을 추가하세요 */
div {
  margin-bottom: 20px;
}

button {
  padding: 10px 20px;
  font-size: 16px;
  cursor: pointer;
}
</style>
