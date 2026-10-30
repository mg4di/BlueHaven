<script setup>
const window = globalThis.window

const tickets = [
  {
    name: 'Tiket Anak',
    price: '35',
    age: 'Usia 3–12 tahun',
    features: ['Akses kolam anak & playground', 'Berlaku 1 hari'],
  },
  {
    name: 'Tiket Dewasa',
    price: '50',
    age: 'Usia 13 tahun ke atas',
    features: ['Akses seluruh area kolam', 'Gratis 1 minuman segar'],
    featured: true,
  },
  {
    name: 'Tiket Keluarga',
    price: '150',
    age: '2 dewasa + 2 anak',
    features: ['Akses penuh untuk 4 orang', 'Hemat hingga 20%'],
  },
]
</script>

<template>
  <section id="harga" class="relative overflow-hidden bg-lagoon px-6 py-24 lg:px-10">
    <div class="absolute -right-20 -top-20 h-80 w-80 rounded-full bg-cyan-200/30 blur-3xl"></div>
    <div class="relative mx-auto max-w-7xl">
      <div class="scroll-reveal text-center">
        <p class="text-sm font-bold uppercase tracking-[.22em] text-ocean">Pilih tiketmu</p>
        <h2 class="mt-3 font-display text-4xl font-bold tracking-tight text-slate-900 md:text-5xl">Liburan seru dimulai di sini</h2>
        <p class="mx-auto mt-4 max-w-xl text-slate-500 leading-7">Pesan online lebih praktis, tanpa antre, dan langsung dapatkan e-ticket di email.</p>
      </div>

      <div class="mt-12 grid gap-6 lg:grid-cols-3">
        <article
          v-for="(ticket, index) in tickets"
          :key="ticket.name"
          class="scroll-reveal pricing-card relative rounded-3xl p-8"
          :class="ticket.featured
            ? 'featured bg-ocean text-white shadow-xl shadow-cyan-900/20 lg:-mt-4'
            : 'bg-white text-slate-900 shadow-sm hover:shadow-lg'"
          :style="{ transitionDelay: `${index * 0.1}s` }"
        >
          <span v-if="ticket.featured" class="absolute right-6 top-6 animate-pulse rounded-full bg-cyan-200 px-3 py-1 text-xs font-bold text-ocean">Terpopuler</span>
          <p class="font-semibold" :class="ticket.featured ? 'text-cyan-100' : 'text-slate-500'">{{ ticket.name }}</p>
          <p class="mt-4 font-display text-4xl font-extrabold">
            Rp{{ ticket.price }}<span class="text-lg font-semibold" :class="ticket.featured ? 'text-cyan-200' : 'text-slate-400'">.000</span>
          </p>
          <p class="mt-2 text-sm" :class="ticket.featured ? 'text-cyan-100' : 'text-slate-500'">{{ ticket.age }}</p>
          <div class="my-7 h-px" :class="ticket.featured ? 'bg-white/20' : 'bg-slate-100'"></div>
          <p v-for="feature in ticket.features" :key="feature" class="flex gap-3 text-sm" :class="ticket.featured ? 'mt-4 text-white first:mt-0' : 'mt-4 text-slate-600 first:mt-0'">
            <iconify-icon icon="lucide:check" class="mt-0.5" :class="ticket.featured ? 'text-cyan-200' : 'text-aqua'"></iconify-icon>
            {{ feature }}
          </p>
          <a
            href="#"
            class="mt-8 flex min-h-12 items-center justify-center rounded-full font-bold transition-all hover:shadow-lg"
            :class="ticket.featured
              ? 'bg-white text-ocean hover:bg-cyan-100'
              : 'border-2 border-aqua text-ocean hover:bg-aqua hover:text-white'"
            @click.prevent="window.navigateTo('select-ticket')"
          >Pilih Tiket</a>
        </article>
      </div>
    </div>
  </section>
</template>
