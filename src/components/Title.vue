<template>
  <h2 class="title">{{ title }}</h2>
  <h6 class="title">{{ sub_title }}</h6>
</template>

<script >
export default {
  name: "TitleComponent",
  props: {
    title: null,
    sub_title: null
  }
}
</script>

<style >

.title {
  margin: 10px;
  color: #898484;
}

</style>
