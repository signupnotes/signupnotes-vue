<script setup lang="ts">
import { onMounted } from 'vue';

onMounted(() => {
  console.log(`the component is now mounted.`);
  const formScript = document.createElement('script');
  formScript.src = 'https://dev.signupnotes-sdk.pages.dev/form.js';
  document.head.appendChild(formScript);
});

const props = defineProps<{
  formId: string;
  returnUrl?: string;
  onCompleted?: (data: Record<string, any>) => void;
  onStepChange?: (step: number) => void;
  onLoading?: (loading: boolean) => void;
  onLoaded?: (loaded: boolean) => void;
  values?: Record<string, any>;
  metaData?: Record<string, any>;
}>();

const handleLoaded = (event: CustomEvent<boolean>) => {
  if (event && props.onLoaded) {
    props.onLoaded(event.detail);
  }
};
const handleLoading = (event: CustomEvent<boolean>) => {
  if (event && props.onLoading) {
    props.onLoading(event.detail);
  }
};
const handleStepChange = (event: CustomEvent<number>) => {
  if (event && props.onStepChange) {
    props.onStepChange(event.detail);
  }
};
const handleCompleted = (event: CustomEvent<Record<string, any>>) => {
  if (event && props.onCompleted) {
    props.onCompleted(event.detail);
  }
};
</script>

<template>
  <form-element
    style="width: 100%; min-height: 100%"
    :form-id="formId"
    :return-url="props.returnUrl"
    @submit-data="handleCompleted"
    @step-change="handleStepChange"
    @loading="handleLoading"
    @loaded="handleLoaded"
    :form-values="JSON.stringify(props.values || {})"
    :meta-data="JSON.stringify(props.metaData || {})"
  />
</template>

<style scoped></style>
