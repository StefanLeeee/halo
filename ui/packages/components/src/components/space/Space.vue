<script lang="ts" setup>
import { computed } from "vue";
import type { Align, Direction, Spacing } from "./interface";
import { SpacingSize } from "./interface";

const props = withDefaults(
  defineProps<{
    spacing?: Spacing;
    direction?: Direction;
    align?: Align;
  }>(),
  {
    spacing: "xs",
    direction: "row",
    align: "center",
  }
);

const wrapperClasses = computed(() => {
  const { direction, align } = props;
  return [`space-direction-${direction}`, `space-align-${align}`];
});
</script>
<template>
  <div
    :class="wrapperClasses"
    :style="`gap: ${SpacingSize[spacing]}px`"
    class="space-wrapper"
  >
    <slot />
  </div>
</template>
<style lang="scss">
.space-wrapper {
  @apply box-border inline-flex;

  &.space-direction-row {
    @apply flex-row;
  }

  &.space-direction-column {
    @apply flex-col;
  }

  &.space-align-center {
    @apply items-center;
  }

  &.space-align-start {
    @apply items-start;
  }

  &.space-align-end {
    @apply items-end;
  }

  &.space-align-stretch {
    @apply items-stretch;
  }
}
</style>
