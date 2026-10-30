<script setup>
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'

const gallery = [
  {
    src: 'https://images.unsplash.com/photo-1654756306479-c0bc0011f7a4?auto=format&fit=crop&w=1600&q=85',
    alt: 'Pemandangan kolam renang dikelilingi pohon palem',
    caption: 'Pemandangan kolam Bluehaven',
  },
  {
    src: 'https://images.unsplash.com/photo-1706843540922-5682f3ad5b98?auto=format&fit=crop&w=1600&q=85',
    alt: 'Anak bermain air di wahana seluncur',
    caption: 'Serunya bermain di wahana air',
  },
  {
    src: 'https://images.unsplash.com/photo-1701361650313-9b20b1d76820?auto=format&fit=crop&w=1600&q=85',
    alt: 'Wahana seluncur air yang berakhir di kolam',
    caption: 'Wahana seluncur yang seru',
  },
  {
    src: 'https://images.unsplash.com/photo-1706843540931-64db8ea7abad?auto=format&fit=crop&w=1600&q=85',
    alt: 'Ibu dan anak bermain bersama di atas pelampung kolam',
    caption: 'Momen bermain bersama keluarga',
  },
  {
    src: 'https://images.unsplash.com/photo-1592484806287-7bc9c8af5405?auto=format&fit=crop&w=1600&q=85',
    alt: 'Dua anak bermain di kolam renang',
    caption: 'Bermain air bersama teman',
  },
]

const track = ref(null)
const activeIndex = ref(0)
let scrollFrame = null

const slides = computed(() => Array.from(track.value?.querySelectorAll('[data-gallery-slide]') ?? []))

function updateActiveIndex() {
  if (!track.value || !slides.value.length) return
  const trackLeft = slides.value[0].offsetLeft
  activeIndex.value = slides.value.reduce((closestIndex, slide, index) => {
    const distance = Math.abs(slide.offsetLeft - trackLeft - track.value.scrollLeft)
    const closestDistance = Math.abs(slides.value[closestIndex].offsetLeft - trackLeft - track.value.scrollLeft)
    return distance < closestDistance ? index : closestIndex
  }, 0)
}

function goTo(index) {
  const slideCount = slides.value.length
  if (!track.value || slideCount === 0) return
  activeIndex.value = (index + slideCount) % slideCount
  track.value.scrollTo({
    left: slides.value[activeIndex.value].offsetLeft - slides.value[0].offsetLeft,
    behavior: 'smooth',
  })
}

function onScroll() {
  if (scrollFrame !== null) return
  scrollFrame = requestAnimationFrame(() => {
    updateActiveIndex()
    scrollFrame = null
  })
}

function onKeydown(event) {
  if (event.key === 'ArrowLeft') {
    event.preventDefault()
    goTo(activeIndex.value - 1)
  } else if (event.key === 'ArrowRight') {
    event.preventDefault()
    goTo(activeIndex.value + 1)
  }
}

onMounted(() => {
  track.value?.addEventListener('scroll', onScroll, { passive: true })
})

onBeforeUnmount(() => {
  track.value?.removeEventListener('scroll', onScroll)
  if (scrollFrame !== null) cancelAnimationFrame(scrollFrame)
})
</script>

<template>
  <section id="galeri" class="mx-auto max-w-7xl px-6 py-24 lg:px-10">
    <div class="scroll-reveal flex items-end justify-between">
      <div><p class="text-sm font-bold uppercase tracking-[.22em] text-ocean">Cerita di Bluehaven</p><h2 class="mt-3 font-display text-4xl font-bold tracking-tight text-slate-900 md:text-5xl">Momen yang tak terlupakan</h2></div>
    </div>
    <div class="mt-10">
      <div
        id="gallery-track"
        ref="track"
        class="gallery-track flex h-[300px] snap-x snap-mandatory gap-4 overflow-x-auto rounded-3xl scroll-smooth sm:h-[420px] lg:h-[500px]"
        role="region"
        aria-label="Galeri foto Bluehaven"
        tabindex="0"
        @keydown="onKeydown"
      >
        <figure v-for="image in gallery" :key="image.src" data-gallery-slide class="relative h-full min-w-full snap-start overflow-hidden rounded-3xl bg-slate-100">
          <img :src="image.src" :alt="image.alt" class="gallery-img h-full w-full object-cover">
          <figcaption class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-slate-950/75 to-transparent px-6 pb-6 pt-20 text-lg font-bold text-white sm:px-10 sm:pb-9">{{ image.caption }}</figcaption>
        </figure>
      </div>
      <div class="mt-5 flex items-center justify-between gap-4">
        <div class="flex items-center gap-2" aria-label="Pilih foto galeri">
          <button
            v-for="(_, index) in gallery"
            :key="index"
            type="button"
            :aria-label="`Tampilkan foto ${index + 1}`"
            :aria-current="activeIndex === index ? 'true' : undefined"
            :class="[
              'h-2.5 rounded-full transition-all hover:bg-ocean',
              activeIndex === index ? 'w-7 bg-ocean' : 'w-2.5 bg-slate-300',
            ]"
            @click="goTo(index)"
          ></button>
        </div>
        <div class="flex gap-2">
          <button type="button" aria-label="Foto sebelumnya" title="Foto sebelumnya" class="flex h-11 w-11 items-center justify-center rounded-full border border-slate-200 text-slate-700 transition hover:border-ocean hover:bg-lagoon hover:text-ocean" @click="goTo(activeIndex - 1)"><iconify-icon icon="lucide:arrow-left" class="text-lg"></iconify-icon></button>
          <button type="button" aria-label="Foto berikutnya" title="Foto berikutnya" class="flex h-11 w-11 items-center justify-center rounded-full border border-slate-200 text-slate-700 transition hover:border-ocean hover:bg-lagoon hover:text-ocean" @click="goTo(activeIndex + 1)"><iconify-icon icon="lucide:arrow-right" class="text-lg"></iconify-icon></button>
        </div>
      </div>
    </div>
  </section>
</template>
