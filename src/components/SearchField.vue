<template>
  <div class="content">
    <md-autocomplete v-model="value" :md-options="suggestions" @md-changed="getSuggestions">
      <label>Suggestion</label>
    </md-autocomplete>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "SearchField",
  props: {
    msg: String
  },
  data: () => ({
    value: null,
    suggestionList: [],
    suggestions: []
  }),
  methods: {
    getSuggestions(searchTerm) {
      var self = this;
      window.setTimeout(() => {
        const term = searchTerm.toLowerCase();
        axios
          .get("http://localhost:8000/suggestions/index/" + term)
          .then(response => {
            this.suggestionList = response.data.data;
            this.suggestions = [];
            this.suggestionList.forEach(function(item) {
              self.suggestions.push(item.name);
            });
          });
      }, 500);
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.content {
  padding-left: 20%;
  width: 80%;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
