<template>
  <div>
    <div class="container">
      <h1 class="title text-center">Dynamic Forms Example</h1>
      <div class="row mt-5">
        <div class="col-6">
          <dynamic-form :id="testForm.id" :fields="testForm.fields" @change="valuesChanged" />
          <div class="row d-flex justify-content-end p-4">
            <button submit="true" :form="testForm.id" class="btn btn-primary">Submit</button>
          </div>
        </div>
        <div class="col-6">
          <pre>{{ formData }}</pre>
          <pre>{{ testForm }}</pre>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import {
  FormField,
  FormValidation,
  required,
  email,
  pattern
} from "@asigloo/vue-dynamic-forms";

const data = () => ({
  formData: {},
  testForm: {
    id: "test-form",
    fields: [
      new FormField({
        type: "text",
        label: "Name",
        name: "name"
      }),
      new FormField({
        type: "email",
        label: "Email",
        name: "email",
        validations: [
          new FormValidation(required, "This field is required"),
          new FormValidation(email, "Format of email is incorrect")
        ]
      }),
      new FormField({
        type: "password",
        label: "Password",
        name: "password",
        validations: [
          new FormValidation(required, "This field is required"),
          new FormValidation(
            pattern(
              "^(?=.*[a-z])(?=.*[A-Z])(?=.*d)(?=.*[#$^+=!*()@%&]).{8,10}$"
            ),
            "Password must contain at least 1 Uppercase, 1 Lowercase, 1 number, 1 special character and min 8 characters max 10"
          )
        ],

        value: "sdsdsd"
      }),
      new FormField({
        type: "textarea",
        label: "Bio",
        name: "bio",
        cols: 30,
        rows: 5
      }),
      new FormField({
        type: "select",
        label: "Category",
        name: "category",
        options: [
          { value: null, text: "Please select an option" },
          { value: "arduino", text: "Arduino" },
          { value: "transistors", text: "Transistors" }
        ]
      }),
      new FormField({
        type: "checkbox",
        label: "Read the conditions",
        name: "conditions",
        inline: false
      }),
      new FormField({
        type: "radio",
        label: "Prefered Animal",
        name: "animal",
        inline: true,
        options: [
          { text: "Dogs", value: "dogs" },
          { text: "Cats", value: "cats" },
          { text: "Others", value: "others" }
        ]
      }),
      new FormField({
        type: "number",
        label: "Number",
        name: "number",
        value: 0
      })
    ]
  }
});

const methods = {
  valuesChanged(values) {
    this.$forceUpdate(); // this is only to refresh the fields on the <pre> tags, not necessary for other purpouses
    this.formData = {
      ...this.formData,
      ...values
    };
  }
};

export default {
  name: "IndexPage",
  data,
  methods
};
</script>

<style>
body {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}

pre {
  font-family: FiraCode, Consolas, Monaco, "Andale Mono", "Ubuntu Mono",
    monospace;
  font-size: 12px;
  color: #fefefe;
  background: #2c3e50;
  border-radius: 4px;
  padding: 0.2rem 0.5rem;
  overflow: auto;
}

.btn {
  display: inline-block;
  font-weight: 400;
  color: #212529;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  user-select: none;
  background-color: transparent;
  border: 1px solid transparent;
  padding: 0.375rem 0.75rem;
  font-size: 1rem;
  line-height: 1.5;
  border-radius: 0.25rem;
}

.btn-primary {
  color: #fff;
  background-color: #007bff;
  border-color: #007bff;
}

.btn-primary:hover {
  background-color: darken(#007bff, 5);
  border-color: darken(#007bff, 5);
}
</style>