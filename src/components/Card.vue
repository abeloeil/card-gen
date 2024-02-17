<template>
  <v-card
    class="mx-auto"
    width="298px"
    height="420px"
    id="card"
    variant="outlined"
    :color="borderColor"
  >
    <v-img
      :src="image ?? 'https://cdn.vuetifyjs.com/images/cards/sunshine.jpg'"
      width="298px"
      :height="imageHeight ?? null"
      max-height="250"
      cover
    ></v-img>

    <v-card-title v-if="showMaj" class="up">
      {{ inputText }}
    </v-card-title>

    <v-card-title v-if="showMin" class="low">
      {{ inputText }}
    </v-card-title>

    <v-card-title v-if="showScript" class="cursed">
      {{ inputText }}
    </v-card-title>
  </v-card>
</template>

<script>
export default {
  props: {
    image: {},
    imageHeight: {},
    borderColor: {},
    inputText: {
      type: String,
      required: true,
    },
    showMaj: {
      type: Boolean,
      required: true,
    },
    showMin: {
      type: Boolean,
      required: true,
    },
    showScript: {
      type: Boolean,
      required: true,
    },
  },
}
</script>

<style lang="scss" scoped>

</style>
