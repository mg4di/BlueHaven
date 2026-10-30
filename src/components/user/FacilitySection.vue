<script setup>
const facilities = [
  {
    icon: 'lucide:waves',
    iconColor: 'text-ocean',
    cardColor: 'bg-lagoon',
    title: 'Kolam Utama',
    description: 'Air jernih dengan area dewasa dan kedalaman yang nyaman.',
  },
  {
    icon: 'lucide:castle',
    iconColor: 'text-blue-500',
    cardColor: 'bg-slate-50',
    title: 'Area Bermain Anak',
    description: 'Wahana air aman dan menyenangkan untuk si kecil.',
  },
  {
    icon: 'lucide:utensils',
    iconColor: 'text-orange-500',
    cardColor: 'bg-slate-50',
    title: 'Restoran',
    description: 'Hidangan lezat dan minuman segar untuk mengisi energi.',
  },
  {
    icon: 'lucide:car-front',
    iconColor: 'text-emerald-500',
    cardColor: 'bg-slate-50',
    title: 'Area Parkir',
    description: 'Parkir luas, aman, dan mudah diakses dari pintu utama.',
  },
]
</script>

<template>
  <section id="fasilitas" class="mx-auto max-w-7xl px-6 py-24 lg:px-10">
    <div class="scroll-reveal flex flex-col justify-between gap-5 md:flex-row md:items-end">
      <div><p class="text-sm font-bold uppercase tracking-[.22em] text-ocean">Semua untuk keseruanmu</p><h2 class="mt-3 font-display text-4xl font-bold tracking-tight text-slate-900 md:text-5xl">Fasilitas yang bikin betah</h2></div>
      <p class="max-w-md text-slate-500 leading-7">Dirancang untuk menghadirkan pengalaman liburan yang nyaman, aman, dan seru untuk seluruh keluarga.</p>
    </div>
    <div class="mt-12 grid gap-5 sm:grid-cols-2 lg:grid-cols-4">
      <article
        v-for="(facility, index) in facilities"
        :key="facility.title"
        class="scroll-reveal facility-card cursor-pointer rounded-3xl p-7"
        :class="facility.cardColor"
        :style="{ transitionDelay: `${index * 0.1}s` }"
      >
        <span class="flex h-14 w-14 items-center justify-center rounded-2xl bg-white shadow-sm" :class="facility.iconColor">
          <iconify-icon :icon="facility.icon" class="text-2xl"></iconify-icon>
        </span>
        <h3 class="mt-7 font-display text-lg font-bold">{{ facility.title }}</h3>
        <p class="mt-3 text-sm leading-6 text-slate-500">{{ facility.description }}</p>
      </article>
    </div>
  </section>
</template>
