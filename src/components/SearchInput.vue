<template>
  <div class="relative">
    <input
      type="text"
      placeholder="Entre le prénom de ton ami ici..."
      class="rounded-md border-gray-900 mt-5 px-5 py-3 shadow-sm w-full focus:outline-none placeholder-gray-500"
      @input="$emit('updateValue', $event.target.value)"
    />
    <div title="Clear Search" class="absolute top-6 right-4 cursor-pointer">
      <svg width="24" height="24" viewBox="0 0 24 24">
        <path
          d="M20 6.91L17.09 4L12 9.09L6.91 4L4 6.91L9.09 12L4 17.09L6.91 20L12 14.91L17.09 20L20 17.09L14.91 12L20 6.91Z"
        />
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    value: {
      type: String,
      required: true,
    },
  },
  emits: ["updateValue"],
  setup() {

  },
};
</script>
