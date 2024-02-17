<template>
  <v-container fluid class="fill-height">
    <v-row>
      <v-col cols="4">
        <card
          :inputText="inputText"
          :showMaj="showMaj"
          :showMin="showMin"
          :showScript="showScript"
          :image="imageUrl"
          :imageHeight="imageHeight"
          :fontSize="fontSize"
          :borderColor="borderColor"
        />
      </v-col>
      <v-col>
        <v-row>
          <v-file-input
            v-model="image"
            prepend-icon="mdi-camera"
            accept="image/*"
            label="Votre image"
            v-on:change="onChange"
          />
        </v-row>
        <v-row>
          <v-text-field
            v-model="inputText"
            label="Texte à insérer"
            required
          ></v-text-field>

        </v-row>
        <v-row>
          <v-col cols="4">
            <v-row>
              <v-checkbox
                v-model="showMaj"
                label="Afficher en majuscule"
              />
            </v-row>
            <v-row>
              <v-checkbox
                v-model="showMin"
                label="Afficher en minuscule"
              />
            </v-row>
            <v-row>
              <v-checkbox
                v-model="showScript"
                label="Afficher en cursive"
              />
            </v-row>
          </v-col>
          <v-col cols="4">
            <div>
              <v-color-picker
                v-model="borderColor"
              />
            </div>
          </v-col>
        </v-row>
        <v-row>
          <v-btn @click="onCapture">
            Export
          </v-btn>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Card from "@/components/Card";
import html2canvas from "html2canvas";

export default {
  data: () => ({
    image: null,
    imageHeight: null,
    imageUrl: null,
    inputText: 'Votre texte',
    showMaj: true,
    showMin: true,
    showScript: true,
    fontSize: 10,
    min: 10,
    max: 20,
    borderColor: "#000000",
  }),

  methods: {
    onChange(e) {
      if (e.target.files[0]) {
        var fr = new FileReader;

        fr.onload = () => { // file is loaded
          var img = new Image;

          img.onload = () => {
            this.imageHeight = img.height / (img.width / 298);
          };

          img.src = fr.result; // is the data URL because called with readAsDataURL
        };

        fr.readAsDataURL(e.target.files[0]);
        this.imageUrl = URL.createObjectURL(e.target.files[0]);

      } else {
        this.imageUrl = null;
      }
    },

    onCapture() {
      html2canvas(document.querySelector("#card")).then(canvas => {
        const link = document.createElement('a');
        link.setAttribute('download', `${this.inputText}.png`);
        link.setAttribute('href', canvas.toDataURL("image/png").replace("image/png", "image/octet-stream"));
        link.click();
      });
    }
  }
}
</script>
