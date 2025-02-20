<script lang="ts" setup>
import personIcon from '@images/misc/person-icon.png'
import type { TmdbPerson } from '@/api/types'
import router from '@/router'

const personProps = defineProps({
  person: Object as PropType<TmdbPerson>,
  width: String,
  height: String,
})

// 当前人物
const personInfo = ref(personProps.person)

// 人物图片是否加载
const isImageLoaded = ref(false)

// 人物图片地址
function getPersonImage() {
  if (!personInfo.value?.profile_path)
    return personIcon
  return `https://image.tmdb.org/t/p/w600_and_h900_bestv2${personInfo.value?.profile_path}`
}

// 人物详情
function goPersonDetail() {
  if (!personInfo.value?.id)
    return
  router.push({
    path: '/person',
    query: {
      personid: personInfo.value?.id,
    },
  })
}
</script>

<template>
  <VHover v-bind="personProps">
    <template #default="hover">
      <VCard
        v-bind="hover.props"
        :height="personProps.height"
        :width="personProps.width"
        class="rounded-lg"
        :class="{
          'transition transform-cpu duration-300 scale-105': hover.isHovering,
        }"
        @click.stop="goPersonDetail"
      >
        <div
          class="person-card relative transform-gpu cursor-pointer rounded text-white shadow ring-1 transition duration-150 ease-in-out scale-100 ring-gray-700"
        >
          <div style="padding-bottom: 150%;">
            <div class="absolute inset-0 flex h-full w-full flex-col items-center p-2">
              <div class="relative mt-2 mb-4 flex h-1/2 w-full justify-center">
                <VAvatar
                  size="120"
                  :class="{
                    'ring-1 ring-gray-700': isImageLoaded,
                  }"
                >
                  <VImg
                    v-img
                    :src="getPersonImage()"
                    cover
                    @load="isImageLoaded = true"
                  />
                </VAvatar>
              </div>
              <div class="w-full truncate text-center font-bold">
                {{ personInfo?.name }}
              </div>
              <div class="overflow-hidden whitespace-normal text-center text-sm" style=" display: -webkit-box; overflow: hidden; -webkit-box-orient: vertical;-webkit-line-clamp: 2;">
                {{ personInfo?.character }}
              </div>
              <div class="absolute bottom-0 left-0 right-0 h-12 rounded-b" />
            </div>
          </div>
        </div>
      </VCard>
    </template>
  </VHover>
</template>

<style lang="scss">
.person-card {
  background-image: linear-gradient(45deg, #99999b, #384359 60%);
}

.person-card:hover {
  background-image: linear-gradient(45deg, #bbbbbd, #8597aa 60%);
}
</style>
