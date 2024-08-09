<template>
  <div>
    <div
      class="hidden lg:block fixed lg:max-w-[295px] w-full overflow-y-auto h-full bg-white z-[999]"
      id="sidebarTM"
    >
      <div class="px-6 py-[50px] gap-y-[50px] flex flex-col">
        <div class="flex items-center justify-between">
          <a href="#" class="flex justify-center">
            <p class="font-bold text-xl">Hi, {{ this.$auth.user.name }}</p>
          </a>
          <a href="#" id="toggleCloseSidebar" class="lg:hidden">
            <svg
              class="w-6 h-6 text-dark"
              fill="none"
              stroke="currentColor"
              viewBox="0 0 24 24"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                stroke-linecap="round"
                stroke-linejoin="round"
                stroke-width="2"
                d="M6 18L18 6M6 6l12 12"
              ></path>
            </svg>
          </a>
        </div>
        <div class="flex flex-col gap-4">
          <NuxtLink :to="{ name: 'tasks' }" class="nav-link active">
            <img src="/assets/svgs/ic-grid.svg" alt="" />
            Task
          </NuxtLink>
          <NuxtLink :to="{ name: 'roles' }" class="nav-link">
            <img src="/assets/svgs/ic-users.svg" alt="" />
            Role
          </NuxtLink>
          <button type="submit" @click="$auth.logout()" class="nav-link">
            <img src="/assets/svgs/ic-signout.svg" alt="" />
            Logout
          </button>
        </div>
      </div>
    </div>
    <Nuxt />
  </div>
</template>
