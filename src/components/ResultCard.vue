<template>
  <li
    class="flex bg-gray-50 hover:bg-gray-100 mb-3 px-4 py-3 rounded-md shadow-md sm:mb-5"
  >
    <img
      class="w-20 h-20 rounded-full"
      :src="avatar"
      alt=""
      width="384"
      height="512"
    />
    <div class="ml-5 flex flex-col justify-between">
      <div class="text-xl font-bold">{{ fullName }}</div>
      <a
        :href="mailtoUrl"
        class="text-blue-600 hover:text-blue-500"
        >{{ email }}</a
      >
    </div>
  </li>
</template>

<script>
import { computed } from "vue";

export default {
  props: {
    result: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    // static values
    const firstName = props.result["first_name"];
    const lastName = props.result["last_name"];
    const email = props.result.email;
    const avatar = props.result.avatar;

    // dynamic values
    const fullName = computed(() => `${firstName} ${lastName}`);
    const mailtoUrl = computed(() => `mailto:${email}`);

    return {
      // static values
      email,
      avatar,
      // dynamic values
      fullName,
      mailtoUrl,
    };
  },
};
</script>
