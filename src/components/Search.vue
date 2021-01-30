 <template>
  <div class="search-bar">
     
          <label>Search Client</label>
          <input type="text" v-model="searchTerm" placeholder="Search Client" v-on:input="handleSearch" >
     
      
        </div>
</template>

<script>
export default {
  name: "Search",
  data() {
    return {
      searchTerm: "",
    };
  },
  methods: {
    handleSearch() {
      this.$emit("input", this.searchTerm);
    },
  },
};
</script>

<style scoped>
</style>>
