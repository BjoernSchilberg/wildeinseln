<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      persistent
      scrollable
      max-width="800">
      <v-card>
        <v-app-bar
          flat
          color="white">
          <v-toolbar-title
            v-if="einsatzstelle.titel"
            class="headline">
            <strong>{{ einsatzstelle.titel }}</strong>
          </v-toolbar-title>
          <v-spacer />
          <v-btn
            fab
            icon
            dark
            color="primary"
            small
            @click="schliessen">
            <v-icon>mdi-close</v-icon>
          </v-btn>
        </v-app-bar>
        <v-sheet
          class="overflow-y-auto"
          max-height="600">
          <v-container>
            <v-img
              v-if="einsatzstelle.foto"
              :aspect-ratio="4.00/1"
              :src="'https://wilde-inseln.nabu-thueringen.de/bilder/'+einsatzstelle.foto" />
            <v-layout row>
              <v-flex md6>
                <v-card-text>
                  <strong> Eckdaten </strong>
                  <ul>
                    <li
                      v-if="einsatzstelle.datum">
                      Erfasst am: <strong>{{ einsatzstelle.datum }}</strong>
                    </li>
                    <li v-if="einsatzstelle.flaeche">
                      Ungefähre Flächengröße in m²:
                      <strong>{{ einsatzstelle.flaeche }}</strong>
                    </li>
                  </ul>
                </v-card-text>

                <v-card-text v-if="einsatzstelle.kurzbeschreibung">
                  <strong>Kurzbeschreibung</strong>
                  <br>
                  {{ einsatzstelle.kurzbeschreibung }}
                </v-card-text>
              </v-flex>
              <v-flex md6>
                <v-card-text
                  v-if="einsatzstelle.institution_ansprechparter || einsatzstelle.vorname_ansprechpartner">
                  <strong>Ansprechpartner</strong>
                  <v-list dense>
                    <v-list-item v-if="einsatzstelle.institution_ansprechparter">
                      <v-list-item-icon>
                        <v-icon color="#0068b4">
                          mdi-home
                        </v-icon>
                      </v-list-item-icon>

                      <v-list-item-content>
                        <v-list-item-title>{{ einsatzstelle.institution_ansprechparter }}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                    <v-list-item v-if="einsatzstelle.vorname_ansprechpartner">
                      <v-list-item-icon>
                        <v-icon color="#0068b4">
                          mdi-account
                        </v-icon>
                      </v-list-item-icon>

                      <v-list-item-content>
                        <v-list-item-title>{{ einsatzstelle.vorname_ansprechpartner }}</v-list-item-title>
                      </v-list-item-content>
                    </v-list-item>
                  </v-list>
                </v-card-text>
              </v-flex>
            </v-layout>
          </v-container>
        </v-sheet>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<style>
.headline {
  word-break: normal !important;
}
</style>

<script>
export default {
  props: { dialog: Boolean, einsatzstelle: {type: Object, default: ()=>{} }},
  methods: {
    schliessen() {
      this.$emit("update:dialog", !this.dialog);
    },
    klick() {
      window.open(this.einsatzstelle.webseite);
      this.$emit("update:dialog", !this.dialog);
      //this.$emit("update:einsatzstelle", this.einsatzstelle={});
    }
  }
};
</script>
