<template>
  <div class="hello">
    <formulate-form v-model="values">
      <FormulateInput type="text" name="title" label="Title" validation="required" />
      <FormulateInput
        type="radio"
        label="Creator Type"
        name="creatorType"
        :options="{
          person: 'Person',
          organisation: 'Organisation'
        }"
      />
      <FormulateInput
        name="creatorName"
        validation="required"
        label="Creator Name"
      />
      <FormulateInput
        type="checkbox"
        name="publisherDifferentFromCreator"
        label="Publisher is different from the Creator"
      />
      <FormulateInput
          type="group"
          name="publisher"
          v-if="values.publisherDifferentFromCreator"
      >
        <FormulateInput
          type="radio"
          label="Publisher Type"
          name="publisherType"
          :options="{
            person: 'Person',
            organisation: 'Organisation'
          }"
        />
        <FormulateInput
          name="publisherName"
          validation="required"
          label="Publisher Name"
        />
      </FormulateInput>
      <FormulateInput
        name="contactPoint"
        validation="required"
        label="Contact Point"
      />
      <FormulateInput
        name="description"
        type="textarea"
        validation="required"
        label="Description"
      />

      <vue-tags-input
        v-model="tag"
        :tags="tags"
        @tags-changed="newTags => tags = newTags"
      />
      <FormulateInput type="submit" label="Save" />
      <pre>{{ values }}</pre>
    </formulate-form>
  </div>
</template>

<script>
import Vue from 'vue'
import VueFormulate from '@braid/vue-formulate'
import VueTagsInput from '@johmun/vue-tags-input'
Vue.use(VueFormulate)

export default {
  name: 'HelloWorld',
  components: {
    VueTagsInput,
  },
  data: function () {
    return {
      values: {},
      tags: [],
      tag: ''
    }
  },
  computed: {
    simpleStringArray() {
      return this.tags.map(tag => tag.text);
    }
  },
  created() {
    this.values.themes = this.simpleStringArray;
  },
  watch: {
    simpleStringArray() {
      this.values.themes = this.simpleStringArray;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
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
