<template>
  <v-card
    class="mx-auto"
    height="500"
  >
    <v-card-text>
      <div>Skripsi 2021</div>
      <p class="text-h4 text--primary">
        Media Pembelajaran Interaktif
      </p>
      <p>Fanny Sarawanti</p>
      <div class="text--primary">
        Teks Prosedur
      </div>
    </v-card-text>
    <v-card-actions>
      <v-btn
        text
        color="teal accent-4"
        @click="reveal = true"
      >
        Learn More
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <v-card
        v-if="reveal"
        class="transition-fast-in-fast-out v-card--reveal"
        style="height: 100%;"
      >
        <v-card-text class="pb-0">
          <p class="text-h4 text--primary">
            Media Pembelajaran Interaktif
          </p>
          <p>Universitas PGRI Yogyakarta</p>
        </v-card-text>
        <v-card-actions class="pt-0">
          <v-btn
            text
            color="teal accent-4"
            @click="reveal = false"
          >
            Close
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-expand-transition>
  </v-card>
</template>

<script>
  export default {
    /*data: () => ({
      reveal: false,
    }),*/
  }
</script>

<style>
.v-card--reveal {
  bottom: 0;
  opacity: 1 !important;
  position: absolute;
  width: 100%;
}
</style>