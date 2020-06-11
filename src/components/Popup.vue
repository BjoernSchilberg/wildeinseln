<template>
  <v-row justify="center">
    <v-dialog
      v-model="dialog"
      persistent
      max-width="800">
      <v-card>
        <v-container>
          <v-img
            v-if="bild"
            :aspect-ratio="4.00/1"
            :src="einsatzstelle.bild" />
          <v-row
            align="end"
            class="lightbox pa-2 fill-height">
            <v-col>
              <div
                v-if="einsatzstelle.titel"
                class="headline">
                <strong>{{ einsatzstelle.titel }}</strong>
              </div>
              <div
                v-if="einsatzstelle.datum"
                class="body-1">
                Erfasst am: <strong>{{ einsatzstelle.datum }}</strong>
              </div>
            </v-col>
          </v-row>
          <v-layout row>
            <v-flex md6>
              <v-card-text>
                <strong> Eckdaten </strong>
                <ul>
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
                v-if="einsatzstelle.ansprechpartner || einsatzstelle.telefon || einsatzstelle.email">
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

        <v-card-actions class="justify-center">
          <v-btn
            small
            color="#0068b4"
            dark
            @click="schliessen">
            Schließen
          </v-btn>
        </v-card-actions>
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
  computed: {
    bild: function() {
      var pattern = new RegExp("^(https?|ftp)://");
      var bild = "";

      if (pattern.test(this.einsatzstelle.bild)) {
        bild = this.einsatzstelle.bild;
      }
      return bild;
    }
  },
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
