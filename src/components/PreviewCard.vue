<script>
export default {
  name: "PreviewCard",
  props: {
    title: null,
    chanel: null,
    image: null,
    id: null
  },
  methods: {
    prepareToPlay(){
      this.$emit('triggerParent',this.id)
    }
  }
}

</script>

<template>
  <v-card
    v-ripple
    class="mx-auto"
    max-width="344"
  >
    <v-img
      :src="image"
      height="200px"
      cover
    ></v-img>

    <v-card-title>
      {{ title }}
    </v-card-title>

    <v-card-subtitle>
      {{ chanel }}
    </v-card-subtitle>

    <v-btn style="padding: 5px; margin-top: 5px" @click="prepareToPlay">
      Play Now
    </v-btn>

    <v-card-actions>
      <v-spacer></v-spacer>
    </v-card-actions>
  </v-card>
</template>
<style>

</style>
