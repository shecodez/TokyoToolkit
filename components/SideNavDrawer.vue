<script setup>
const openNavDrawer = ref(false)
function openDrawer() {
  openNavDrawer.value = true
}
function closeDrawer() {
  openNavDrawer.value = false
}

const navLinks = ref([
  { link: '/about', label: 'About' },
  {
    link: '/events',
    label: 'Events',
    dropdown: true,
    isOpen: false,
    menu: [
      { link: '/events/all', label: 'All' },
      { link: '/events/workshops', label: 'Workshops' },
    ],
  },
  { link: '/blog', label: 'Blog' },
  {
    link: '/shop',
    label: 'Shop',
    dropdown: true,
    isOpen: false,
    menu: [
      { link: { path: '/shop', query: { category: 'men\'s clothing' } }, label: 'Men\'s Clothing' },
      { link: { path: '/shop', query: { category: 'women\'s clothing' } }, label: 'Women\'s Clothing' },
    ],
  },
  { link: '/contact', label: 'Contact' },
])

const socialIcons = [
  {
    icon: 'i-carbon:logo-discord',
    label: 'Discord',
    link: 'https://discord.gg/x2tr4fJu',
  },
  { icon: 'i-carbon:logo-instagram', label: 'Instagram', link: 'https://www.instagram.com/TokyoToolkit/' },
  { icon: 'i-carbon:logo-twitter', label: 'Twitter', link: 'https://twitter.com/TokyoToolkit' },
  { icon: 'i-carbon:logo-youtube', label: 'YouTube', link: 'https://www.youtube.com/channel/UCzV2BYxwNJlgc67Szapji0g' },
  { icon: 'i-carbon:logo-pinterest', label: 'Pinterest', link: 'https://www.pinterest.com/tokyotoolkit/' },
]
</script>

<template>
  <client-only>
    <button title="Menu" class="flex" @click="openDrawer">
      <slot />
      <span class="sr-only">Menu</span>
    </button>

    <Drawer :is-open="openNavDrawer" css="w-80 mr-auto shadow-lg bg-white dark:bg-black" @close="closeDrawer">
      <div class="side-nav relative py-4 flex flex-col items-center h-full text-center">
        <button class="absolute top-4 right-4" @click="closeDrawer">
          <div class="i-carbon:close" />
        </button>

        <div class="site-logo rainbow-text">
          Tokyo<span class="heading-font">Toolkit</span>
        </div>

        <nav class="slice-anim my-8 flex-1 w-full">
          <ul class="menu flex flex-col">
            <template v-for="(n, i) in navLinks" :key="`main-nav-link-${i}`">
              <li class="group relative">
                <div class="slice-line">
                  <NuxtLink :to="n.link" :data-text="n.label" class="slice nav-link" :class="n.dropdown && 'dropdown'">
                    {{ n.label }}
                    <span v-if="n.dropdown" class="dots" />
                  </NuxtLink>
                </div>
                <div v-if="n.dropdown" class="dropdown-menu slice-anim group-hover:block h-auto hidden">
                  <ul class="menu top-0 w-full bg-gray-300 dark:bg-black shadow-lg py-3 border-y">
                    <template v-for="(d, i) in n.menu" :key="`dropdown-${n.label}-li-${i}`">
                      <div class="slice-line">
                        <li class="hover:text-teal-600">
                          <NuxtLink :to="d.link" :data-text="d.label" class="slice px-4 py-2 block">
                            {{ d.label }}
                          </NuxtLink>
                        </li>
                      </div>
                    </template>
                  </ul>
                </div>
              </li>
            </template>
          </ul>
        </nav>

        <div class="uppercase flex flex-col divide-y space-y-3 divide-primary py-6">
          <h2 class="text-3xl">
            Connect&nbsp;<span class="text-teal-500 text-lg">with</span>&nbsp;Us
          </h2>
          <ul class="flex justify-center gap-4 text-xl pt-3">
            <li v-for="(s, i) in socialIcons" :key="`sidenav-social-icon-${i}`" :title="s.label">
              <a :href="s.link" target="_blank" class="link"><div :class="s.icon" /></a>
            </li>
          </ul>
        </div>

        <div class="flex flex-col pb-4">
          <p class="text-xs md:text-sm">
            &copy; {{ new Date().getFullYear() }}
            <span class="text-teal-500">Tokyo<span class="heading-font">Toolkit</span></span>
            All Rights Reserved.
          </p>
          <div class="divide-x divide text-xs md:text-sm">
            <NuxtLink to="/legal/privacy" class="link pr-2">
              Privacy Policy
            </NuxtLink>
            <NuxtLink to="/legal/terms" class="link pl-2">
              Terms of Use
            </NuxtLink>
          </div>
        </div>

        <div class="flex items-center justify-center gap-1 text-xs">
          Made with <div class="i-carbon:favorite-filled" /> by
          <a href="https://shecodez.com" target="_blank" class="link">shecodez</a> | NJN
        </div>
      </div>
    </Drawer>
  </client-only>
</template>

<style scoped>
/* .side-nav {
  @apply relative py-4 flex flex-col items-center h-full;
} */

.site-logo {
  @apply text-4xl pt-10 pb-3 font-black;
}

.nav-link {
  @apply flex font-semibold text-xl tracking-wider p-4;
}

.link {
  font-family: 'Marcellus SC', Georgia, serif;
  @apply text-teal-500 hover:text-teal-700 cursor-pointer;
}

/* strike-through animation links */
.slice-anim ul.menu a.slice {
  color: transparent;
}
.slice-anim a {
  white-space: nowrap;
  font-family: 'Marcellus SC', Georgia, serif;
  transition: 0.5s;
  position: relative;
  font-weight: 500 !important;
}
.slice-anim a:before,
.slice-anim a:after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  transition: 0.5s;
  transition-delay: 0.25s;
}
.slice-anim a:before {
  -webkit-clip-path: polygon(0 0, 100% 0, 100% 50%, 0 50%);
  clip-path: polygon(0 0, 100% 0, 100% 50%, 0 50%);
}
.slice-anim a:after {
  -webkit-clip-path: polygon(0 50%, 100% 50%, 100% 100%, 0 100%);
  clip-path: polygon(0 50%, 100% 50%, 100% 100%, 0 100%);
}
.slice-anim a:hover:before {
  transform: translateX(2px);
}
.slice-anim a:hover:after {
  opacity: 1 !important;
  transform: translateX(-2px);
}
.slice-anim ul.menu .slice-line {
  @apply relative overflow-hidden;
}
.slice-anim ul.menu .slice-line:before {
  content: '';
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 100%;
  height: 1px;
  left: -100%;
  transition: 0.5s;
  @apply bg-teal-500;
}
.slice-anim ul.menu .slice-line:hover:before {
  left: 100%;
}

ul.menu > li a:before,
ul.menu > li a:after,
ul.menu > li span.dots:before,
ul.menu > li span.dots:after {
  padding: inherit;
  color: black;
}
.dark ul.menu > li a:before,
.dark ul.menu > li a:after,
.dark ul.menu > li span.dots:before,
.dark ul.menu > li span.dots:after {
  padding: inherit;
  color: white;
}
ul.menu li a:hover:before,
ul.menu li a:hover:after,
ul.menu li:hover span.dots:before,
ul.menu li:hover span.dots:after {
  @apply text-teal-500;
}

ul.menu li a.router-link-exact-active:before,
ul.menu li a.router-link-exact-active:after {
  @apply text-teal-500;
}

.dropdown span.dots:after {
  content: '';
  position: absolute;
  display: block;
  bottom: 0;
  top: 50%;
  right: 10%;
  width: 3px;
  height: 3px;
  margin-left: -1px;
  border-radius: 1.5px;
  box-shadow: 5px 0 0 0, -5px 0 0 0, inset 0 0 0 3px;
  opacity: 0.4;
  transition: 0.2s opacity;
}
</style>
