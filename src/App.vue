<script setup lang="ts">
import {ref} from "vue";
import ProductCard from "./components/ProductCard.vue";
import type {Product} from "./types/product";

const ourProducts: Product[] = [
  {
    id: 1,
    image: "https://freepngimg.com/save/17464-teddy-bear-png-picture/528x513",
    imageSrc: "FreePNGimg",
    name: "Karla Krammebjørn",
    price: 249,
    description:
      "En klassisk, blød og karamelfarvet bamse, der elsker lange kram.",
    inStock: true,
  },
  {
    id: 2,
    image:
      "https://static.vecteezy.com/system/resources/previews/048/386/675/non_2x/a-brown-teddy-bear-sitting-upright-isolated-on-a-transparent-background-free-png.png",
    imageSrc: "Vecteezy",
    name: "Bruno Bamse",
    price: 199,
    description:
      "En sød, brun sidde-bamse, der er klar til at blive din nye ven.",
    inStock: true,
  },
  {
    id: 3,
    image:
      "https://static.vecteezy.com/system/resources/previews/058/174/840/non_2x/teddy-bear-holding-a-heart-symbolizes-love-and-comfort-on-a-pure-transparent-background-for-special-moments-teddy-bear-with-heart-isolated-on-white-background-free-png.png",
    imageSrc: "Vecteezy",
    name: "Hjerteven Hugo",
    price: 279,
    description: "En kærlig bamse med et hjerte, perfekt som en blød gave.",
    inStock: true,
  },
  {
    id: 4,
    image: "https://www.pngkey.com/png/full/2-26452_teddy-bear-png.png",
    imageSrc: "PNGkey",
    name: "Bella Bamse",
    price: 179,
    description: "En hyggelig lille bamse med et venligt blik og blød pels.",
    inStock: true,
  },
  {
    id: 5,
    image:
      "https://static.vecteezy.com/system/resources/previews/048/387/096/non_2x/a-white-teddy-bear-sitting-upright-isolated-on-a-transparent-background-free-png.png",
    imageSrc: "Vecteezy",
    name: "Snefnug",
    price: 259,
    description: "En fin, hvid bamse med blød pels, der spreder vinterhygge.",
    inStock: false,
  },
  {
    id: 6,
    image: "https://www.freeiconspng.com/uploads/teddy-bear-png-24.png",
    imageSrc: "Free Icons PNG",
    name: "Luna",
    price: 189,
    description: "En nuttet klassisk bamse, der passer perfekt til godnatkram.",
    inStock: true,
  },
  {
    id: 7,
    image:
      "https://png.pngtree.com/png-clipart/20231211/original/pngtree-toy-teddy-bear-isolated-photo-png-image_13820206.png",
    imageSrc: "Pngtree",
    name: "Tulle",
    price: 229,
    description: "En blød legebamse, som altid er klar på et lille eventyr.",
    inStock: true,
  },
  {
    id: 8,
    image:
      "https://www.freepnglogos.com/uploads/teddy-bear-png/photo-teddy-bear-furry-teddy-bear-bear-16.png",
    imageSrc: "Freepnglogos",
    name: "Fnuller",
    price: 269,
    description: "En ekstra fluffy bamse, der er uimodståelig at putte med.",
    inStock: false,
  },
  {
    id: 13,
    image:
      "https://static.vecteezy.com/system/resources/thumbnails/034/798/380/small_2x/ai-generated-brown-teddy-bear-isolated-on-transparent-background-png.png",
    imageSrc: "Vecteezy",
    name: "Karamel",
    price: 199,
    description:
      "En klassisk brun bamse med blød pels og masser af plads til kram.",
    inStock: true,
  },
];

//ref gør at vi kan tilføje flere produkter fx til kurv - den referer mellem tal og funktioner, så vi kan lave dynamiske opdateringer

const cartCount = ref<number>(0);

function addToCart(product: Product): void {
  if (product.inStock) {
    cartCount.value++;
  }
}

const message: string = "Bamsebo – bløde venner til store kram";

const productPrice: number = 14999;
const discount: number = 0;
const discountPercentage: number = 20;

function calculatePrice(product: Product, discount: number): number {
  return product.price - discount;
}

function calculateDiscountPrice(price: number, discount: number): number {
  return price - price * (discount / 100);
}

function showPrice(): void {
  // console.log("Pris: " + calculatePrice(productPrice, discount));
  ourProducts.forEach((product) => {
    console.log(
      `Pris for ${product.name}: ${calculatePrice(product, discount)}`,
    );
  });
  console.log(
    "Pris: " + calculateDiscountPrice(productPrice, discountPercentage),
  );
}

// const calculatedProductPrice = calculatePrice(ourProduct - discount);
const calculatedProductPrices = ourProducts.map((product) =>
  calculatePrice(product, discount),
);

const discountedPrice = calculateDiscountPrice(
  productPrice,
  discountPercentage,
);

showPrice();
</script>

<template>
  <div
    class="mx-auto flex min-h-screen w-full max-w-7xl flex-col gap-8 px-4 py-8 sm:px-6 lg:px-8"
  >
    <h1
      class="rounded-3xl border border-[var(--color-border)] bg-[var(--color-surface)] px-5 py-8 text-center text-3xl font-extrabold tracking-tight text-[var(--color-accent)] shadow-[0_12px_35px_var(--color-shadow)] sm:px-8 sm:py-10 sm:text-5xl"
    >
      {{ message }}
    </h1>
    <div class="grid grid-cols-1 gap-5 sm:grid-cols-2 lg:grid-cols-3">
      <p
        class="rounded-2xl border border-[var(--color-border)] bg-[var(--color-surface)] p-4 text-center font-semibold text-[var(--color-text)] shadow-sm sm:col-span-2 lg:col-span-3"
      >
        Antal varer i kurven: {{ cartCount }}
      </p>
      <ProductCard
        v-for="product in ourProducts"
        :key="product.id"
        :product="product"
        :price="calculatePrice(product, discount)"
        @add-to-cart="addToCart"
      />
      <p
        class="rounded-2xl border border-[var(--color-border)] bg-[var(--color-surface)] p-4 text-center font-semibold text-[var(--color-text)] shadow-sm sm:col-span-2 lg:col-span-3"
      >
        Antal varer i kurven: {{ cartCount }}
      </p>
    </div>

    <!-- product er type-annoteringen, ourProduct er produktet -->

    <!-- <div class="bg-white rounded-xl p-5 text-black my-5">
    <p>Produkt prisen:{{ productPrice }}</p>
    <p>Rabatten: {{ discount }} kr</p>
    <p>Så er prisen: {{ productPrice - discount }}</p>

    <br />

    <p>Hvis rabatten er {{ discountPercentage }}%</p>
    <p>Så er prisen: {{ discountedPrice }}</p>
    <p>{{ ourProduct.name }}</p>
    <p>Pris: {{ calculatedProductPrice }} kr.</p>
  </div> -->
  </div>
</template>
