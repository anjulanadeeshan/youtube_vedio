<template>
  <div style="height: 75vh ">
    <TitleComponent title="Numbers Api" sub_title=" Let your metrics tell tales with our API of number facts "/>
  </div>
</template>

<script>
import TitleComponent from "@/components/Title.vue";

export default {
  name: "NumbersApi",
  components: {TitleComponent}
}
</script>

<style>
.title {
  margin: 10px;
  color: gray;
}
</style>
