<script lang="tsx" setup>
import "./styles/index.scss";
import { ref, watch, onMounted, onUnmounted } from "vue";
import Highcharts from "highcharts";
import Highcharts3d from "highcharts/highcharts-3d";
Highcharts3d(Highcharts);

const props = defineProps<{
  options?: Highcharts.Options;
}>();
let highchartsOptions = ref<Highcharts.Options>(props.options || {});
let highchartsInstance: Highcharts.Chart | null = null;
const rootRef = ref<HTMLElement>();

function getHighchartsClass(): typeof Highcharts {
  return Highcharts;
}
function getHighchartsInstance(): Highcharts.Chart | null {
  return highchartsInstance;
}
function getHighchartsOptions(): Highcharts.Options {
  return highchartsOptions.value;
}
function setOptions(
  options: Highcharts.Options,
  update: boolean,
  redraw: boolean = true
) {
  highchartsOptions.value = options;
  highchartsInstance?.update(options, update, redraw);
}

watch(
  () => props.options,
  (options: Highcharts.Options | undefined) => {
    if (options) {
      setOptions(options, true, true);
    }
  }
);

onMounted(() => {
  highchartsInstance = Highcharts.chart(rootRef.value!, highchartsOptions.value);

  const resize = () => {
    highchartsInstance?.reflow();
  };
  window.addEventListener("resize", resize);

  onUnmounted(() => {
    window.removeEventListener("resize", resize);
    highchartsInstance?.destroy();
  });
});

defineExpose({
  getHighchartsClass,
  getHighchartsInstance,
  getHighchartsOptions,
  setOptions,
});
</script>

<template>
  <main ref="rootRef" class="dyn-component--vue dyn-highcharts"></main>
</template>

<style lang="scss" scoped></style>
