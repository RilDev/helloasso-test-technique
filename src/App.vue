<template>
  <main class="p-8 max-w-lg mx-auto">
    <div class="text-center text-3xl font-bold">Mon ami s'appelle...</div>
    <SearchInput :value="value" @updateValue="findFirstName"></SearchInput>
    <ul class="mt-5">
      <ResultCard v-for="result in results"
      :key="result.id"
      :result="result"
      ></ResultCard>
    </ul>
  </main>
</template>

<script>
import SearchInput from "/src/components/SearchInput.vue";
import ResultCard from "/src/components/ResultCard.vue";
import axios from "axios";
import debounce from "lodash/debounce";

const {
  data: { data: rawResultList },
} = await axios.get(`https://reqres.in/api/users`);

export default {
  components: {
    SearchInput,
    ResultCard,
  },
  setup() {
    // dynamic values
    const searchValue = "";
    const results = rawResultList;

    // methods
    const findFirstName = debounce((value) => {
      console.log(value);
    }, 300);
    return {
      // dynamic values
      searchValue,
      results,
      // methods
      findFirstName,
    };
  },
};
</script>
