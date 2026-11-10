<script setup lang="ts">
import type {Product} from "../types/product";
defineProps<{
  product: Product;
  price: number;
}>();

const emit = defineEmits<{
  addToCart: [product: Product];
}>();
</script>

<template>
  <article
    class="flex h-full flex-col gap-4 rounded-3xl border border-[var(--color-border)] bg-[var(--color-surface)] p-4 text-[var(--color-text)] shadow-[0_8px_24px_var(--color-shadow)] transition duration-200 hover:-translate-y-1 hover:shadow-[0_14px_32px_var(--color-shadow)] sm:p-5"
  >
    <h2 class="text-xl font-bold text-[var(--color-text)] sm:text-2xl">{{ product.name }}</h2>
    <p class="text-3xl font-extrabold text-[var(--color-accent)] sm:text-4xl">
      {{ price }} kr.
    </p>
    <img
      :src="product.image"
      :alt="product.name"
      :title="product.imageSrc"
      class="h-48 w-full rounded-2xl bg-[var(--color-image)] p-3 object-contain sm:h-56"
    />
    <p class="flex-1 leading-relaxed text-[var(--color-muted)]">
      {{ product.description }}
    </p>
    <p
      v-if="product.inStock"
      class="rounded-xl bg-[var(--color-stock-bg)] p-2 text-center font-semibold text-[var(--color-stock)]"
    >
      På lager
    </p>
    <p
      v-else
      class="rounded-xl bg-[var(--color-sold-bg)] p-2 text-center font-semibold text-[var(--color-sold)]"
    >
      Udsolgt
    </p>
    <button
      class="rounded-full bg-[var(--color-accent)] px-5 py-3 font-bold text-white transition hover:bg-[var(--color-accent-hover)] focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[var(--color-accent)] disabled:cursor-not-allowed disabled:bg-[var(--color-disabled)] disabled:text-[var(--color-muted)]"
      @click="emit('addToCart', product)"
      :disabled="!product.inStock"
    >
      Læg i kurv
    </button>
  </article>
</template>
