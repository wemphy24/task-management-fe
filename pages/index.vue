<template>
  <div class="flex items-center justify-center">
    <section class="py-[50px] flex flex-col items-center justify-center px-4">
      <div class="text-[32px] font-semibold text-dark mt-[70px]">
        Task Management App
      </div>
      <p class="my-4 text-base leading-7 text-center text-grey">
        Manage your task with your team
      </p>

      <NuxtLink to="/tasks" class="w-full btn btn-primary mt-4">
        Create Task
      </NuxtLink>
      <NuxtLink to="/login" class="w-full btn btn-primary mt-4">
        Try App
      </NuxtLink>
    </section>
  </div>
</template>
