<template>
    <div>
      okok
      <form v-on:submit.prevent="onSubmit">
          <vueform
            v-model="model"
            :schema="schema"
            :ui-schema="uiSchema"

          >
        </vueform>

        <button type="submit">GO</button>
      </form>
    </div>
</template>

<script>
  import VueFormJsonSchema from 'vue-form-json-schema';

  import fields from './fields.json'
  import axios from 'axios'

  // Vue.component('vue-form-json-schema', VueFormJsonSchema);
  export default {
    components: {
      vueform: VueFormJsonSchema
    },
    methods: {
      onSubmit() {
        console.log(111111111, { ...this.model});
        axios.post('http://iplink-form.free.beeceptor.com', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
      },
      loadFields() {
        // axios.get('http://iplink-form.free.beeceptor.com')
        //       .then(response => {
        //         console.log(response);
        //         this.schema.properties = response.data.properties;
        //         this.uiSchema = response.data.uiSchema;
        //       })

        this.schema.properties = fields.properties;
                this.uiSchema = fields.uiSchema;
      }
    },
    data() {
      return {
        // An object which holds the form values
        model: {},
        // A valid JSON Schema object
        schema: {
          type: 'object',
          properties: {},
        },
        // Array of HTML elements or Vue components
        uiSchema: [],
      };
    },
    mounted() {
      this.loadFields();
    }
  };
</script>