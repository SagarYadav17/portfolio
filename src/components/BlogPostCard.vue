<script>
export default {
  props: {
    data: {},
  }
}
</script>

<template>
  <article class="rounded-xl bg-white p-4 ring ring-indigo-50 sm:p-6 lg:p-8">
    <div class="flex items-start sm:gap-8">
      <div>
        <h3 class="mt-4 text-lg font-medium sm:text-xl">
          <a href="" class="hover:underline"> {{ data.title }} </a>
        </h3>

        <p class="mt-1 text-sm text-gray-700">
          {{ data.brief }}
        </p>

        <div class="mt-4 sm:flex sm:items-center sm:gap-2">
          <div class="flex items-center gap-1 text-gray-500">
            <svg class="h-4 w-4" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                d="M12 8v4l3 3m6-3a9 9 0 11-18 0 9 9 0 0118 0z"></path>
            </svg>

            <p class="text-xs font-medium">{{ data.dateAdded }}</p>
          </div>
        </div>
      </div>
    </div>
  </article>
</template>

