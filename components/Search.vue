<template>
  <div>
    <b-input-group class="mt-3">
      <b-form-input type="search" input="search" placeholder="Search" required></b-form-input>
      <b-input-group-append>
        <b-button variant="dark">Button</b-button>
      </b-input-group-append>
    </b-input-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      search: "",
    };
  },
};
</script>
