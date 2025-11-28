<script setup lang="ts">
  import { buttonVariants } from '.'
  import { Primitive } from 'reka-ui'

  import type { ButtonVariants } from '.'
  import type { HTMLAttributes } from 'vue'

  import { cn } from '@/lib/utils'

  interface Props {
    variant?: ButtonVariants['variant']
    size?: ButtonVariants['size']
    class?: HTMLAttributes['class']
    as?: string
    asChild?: boolean
  }

  const props = withDefaults(defineProps<Props>(), {
    as: 'button',
    asChild: false
  })
</script>

<template>
  <Primitive
    :as="props.as"
    :as-child="props.asChild"
    :class="cn(buttonVariants({ variant, size }), props.class)"
  >
    <slot />
  </Primitive>
</template>
