<template>
  <main class="p-8 max-w-lg mx-auto">
    <div class="text-center text-3xl font-bold">Mon ami s'appelle...</div>
    <SearchInput
      v-model:value="searchValue"
      @updateValue="findFirstName"
      @clearSearch="clearSearch"
    ></SearchInput>
    <ul class="mt-5">
      <ResultCard
        v-for="result in results"
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
import { ref } from "vue";

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
    const searchValue = ref("");
    const results = ref([]);

    // methods
    const findFirstName = debounce((inputSearch) => {
      // reset results when no search
      if (inputSearch === "") {
        results.value = [];
      } else {
        // filter the raw input list to find results
        results.value = rawResultList.filter((profile) =>
          profile["first_name"]
            .toLowerCase()
            .includes(inputSearch.toLowerCase())
        );
      }
    }, 300);

    function clearSearch() {
      searchValue.value = "";
      results.value = [];
    }
    return {
      // dynamic values
      searchValue,
      results,
      // methods
      findFirstName,
      clearSearch,
    };
  },
};
</script>
