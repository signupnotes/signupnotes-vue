<script setup lang="ts">
import { onMounted } from 'vue';

onMounted(() => {
  const formScript = document.createElement('script');
  if (document.querySelector('[src="https://sdk.signupnotes.com/form.js"]')) return;
  formScript.src = 'https://sdk.signupnotes.com/form.js';
  document.head.appendChild(formScript);
});

const props = defineProps<{
  formId: string;
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
  <signup-notes
    style="width: 100%; min-height: 100%"
    :form-id="formId"
    @submit-data="handleCompleted"
    @step-change="handleStepChange"
    @loading="handleLoading"
    @loaded="handleLoaded"
    :form-values="JSON.stringify(props.values || {})"
    :meta-data="JSON.stringify(props.metaData || {})"
  />
</template>

<style scoped></style>
