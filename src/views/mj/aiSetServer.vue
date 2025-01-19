<script setup lang="ts">
import { NInput, NButton, useMessage,NSwitch } from "naive-ui" //NInfiniteScroll
 
import {gptServerStore} from '@/store'
import { mlog, myTrim,blurClean} from "@/api";
import { t } from '@/locales'
import {  watch } from "vue";

const emit= defineEmits(['close']);
const ms= useMessage();
const save = ()=>{
    gptServerStore.setMyData( gptServerStore.myData );
    ms.success( t('mjchat.success'));
    emit('close');
}
// const blurClean= ()=>{
//   mlog('blurClean');
//   gptServerStore.myData.OPENAI_API_BASE_URL =myTrim( myTrim(gptServerStore.myData.OPENAI_API_BASE_URL.trim(),'/'), '\\' );
//   gptServerStore.myData.OPENAI_API_KEY = gptServerStore.myData.OPENAI_API_KEY.trim();
//   gptServerStore.myData.MJ_SERVER =myTrim( myTrim( gptServerStore.myData.MJ_SERVER.trim(),'/'),'\\');
//   gptServerStore.myData.MJ_API_SECRET = gptServerStore.myData.MJ_API_SECRET.trim();
//   gptServerStore.myData.UPLOADER_URL=  myTrim( myTrim( gptServerStore.myData.UPLOADER_URL.trim(),'/'),'\\');
// }

//const isSync= computed(()=>gptServerStore.myData.IS_SET_SYNC )
watch(() => gptServerStore.myData.OPENAI_API_BASE_URL , (n)=>{
   if(!gptServerStore.myData.IS_SET_SYNC) return  ;
    gptServerStore.myData.MJ_SERVER= n
    gptServerStore.myData.SUNO_SERVER=n;
    gptServerStore.myData.LUMA_SERVER=n;
    gptServerStore.myData.VIGGLE_SERVER=n;
    gptServerStore.myData.RUNWAY_SERVER=n;
    gptServerStore.myData.IDEO_SERVER=n;
    gptServerStore.myData.KLING_SERVER=n;
    gptServerStore.myData.PIKA_SERVER=n;
    gptServerStore.myData.PIXVERSE_SERVER=n;
    gptServerStore.myData.UDIO_SERVER=n;
});
watch(() => gptServerStore.myData.OPENAI_API_KEY , (n)=>{
    if(!gptServerStore.myData.IS_SET_SYNC) return  ;
    gptServerStore.myData.MJ_API_SECRET= n
    gptServerStore.myData.SUNO_KEY=n;
    gptServerStore.myData.LUMA_KEY=n;
    gptServerStore.myData.VIGGLE_KEY=n;
    gptServerStore.myData.RUNWAY_KEY=n;
    gptServerStore.myData.IDEO_KEY=n;
    gptServerStore.myData.KLING_KEY=n;
    gptServerStore.myData.PIKA_KEY=n;
    gptServerStore.myData.PIXVERSE_KEY=n;
    gptServerStore.myData.UDIO_KEY=n;
});
</script>
<template>
<div id="setserver"> 

  <div  class="w-full h-[540px] overflow-y-auto overflow-x-hidden">
    <div class="p-2">
      <div class="flex justify-between items-baseline ">
        <div class="text-right">{{ $t('mj.setOpen') }}</div>

        </div>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input @blur="blurClean"  :placeholder="$t('mj.setOpenPlaceholder') " v-model:value="gptServerStore.myData.OPENAI_API_BASE_URL" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">{{ $t('mj.setOpenUrl') }}:</span>
            </template>
          </n-input>
      </section>

      <section class="mb-4 flex justify-between items-center"  >
          <n-input  @blur="blurClean" type="password"  :placeholder="$t('mj.setOpenKeyPlaceholder')" show-password-on="click" v-model:value="gptServerStore.myData.OPENAI_API_KEY" clearable>
            <template #prefix>
              <span class="text-[var(--n-tab-text-color-active)]">OpenAI Api Key:</span>
            </template>
          </n-input>
      </section>
    </div>
  </div>

  <section class=" text-right flex justify-end space-x-2"  >
      <NButton   @click="gptServerStore.setInit()">{{$t('mj.setBtBack')}}</NButton>
      <NButton type="primary" @click="save">{{$t('mj.setBtSave')}}</NButton>
  </section>
</div>
</template>
<style>
#setserver .n-input .n-input__input-el{
    text-align: right;
}
</style>