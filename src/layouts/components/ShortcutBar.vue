<script lang="ts" setup>
import NameTestView from '@/views/system/NameTestView.vue'
import NetTestView from '@/views/system/NetTestView.vue'

// App捷径
const appsMenu = ref(false)

// 名称测试弹窗
const nameTestDialog = ref(false)

// 网络测试弹窗
const netTestDialog = ref(false)
</script>

<template>
  <VMenu
    v-model="appsMenu"
    max-width="600"
    width="340"
    max-height="560"
    location="top end"
    origin="top end"
    transition="scale-transition"
    close-on-content-click
  >
    <!-- Menu Activator -->
    <template #activator="{ props }">
      <IconBtn
        class="me-2"
        v-bind="props"
      >
        <VIcon icon="mdi-checkbox-multiple-blank-outline" />
      </IconBtn>
    </template>
    <!-- Menu Content -->
    <VCard>
      <VCardItem class="border-b">
        <VCardTitle>捷径</VCardTitle>
        <template #append>
          <IconBtn @click="() => {}">
            <VIcon icon="mdi-checkbox-multiple-blank-outline" />
          </IconBtn>
        </template>
      </VCardItem>
      <div class="ps ps--active-y">
        <VRow class="ma-0 mt-n1">
          <VCol
            cols="6"
            class="text-center cursor-pointer pa-0 shortcut-icon border-e"
          >
            <VListItem
              class="pa-4"
              @click="nameTestDialog = true"
            >
              <VAvatar
                size="48"
                variant="tonal"
              >
                <VIcon icon="mdi-text-recognition" />
              </VAvatar>
              <h6 class="text-base font-weight-medium mt-2 mb-0">
                识别
              </h6>
              <span class="text-sm">名称识别测试</span>
            </VListItem>
          </VCol>
          <VCol
            cols="6"
            class="text-center cursor-pointer pa-0 shortcut-icon"
            @click="() => {}"
          >
            <VListItem
              class="pa-4"
              @click="netTestDialog = true"
            >
              <VAvatar
                size="48"
                variant="tonal"
              >
                <VIcon icon="mdi-network-outline" />
              </VAvatar>
              <h6 class="text-base font-weight-medium mt-2 mb-0">
                网络
              </h6>
              <span class="text-sm">测试网速连通性</span>
            </VListItem>
          </VCol>
        </VRow>
      </div>
    </VCard>
  </VMenu>
  <!-- 名称测试弹窗 -->
  <VDialog
    v-model="nameTestDialog"
    max-width="800"
  >
    <VCard title="名称识别测试">
      <DialogCloseBtn @click="nameTestDialog = false" />
      <VCardItem>
        <NameTestView />
      </VCardItem>
    </VCard>
  </VDialog>
  <!-- 网络测试弹窗 -->
  <VDialog
    v-model="netTestDialog"
    max-width="600"
  >
    <VCard title="网络测试">
      <DialogCloseBtn @click="netTestDialog = false" />
      <VCardItem>
        <NetTestView />
      </VCardItem>
    </VCard>
  </VDialog>
</template>
