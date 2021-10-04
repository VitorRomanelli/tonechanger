<template>
  <div
    class="pa-4 d-flex justify-center align-center"
    style="background: #100C1C; height: 100%"
  >
    <v-card class="pa-8" color="#fff" max-width="500" style="border-radius: 10px; box-shadow: 8px 8px 0px #21d7af;">
      <v-card-title class="d-flex flex-column justify-center align-center mb-3">
        <h2>Jam</h2>
        <h3>
        Tone Changer
        </h3>
      </v-card-title>

      <v-textarea
        class="mb-3"
        style="resize: vertical; border-radius: 8px;"
        color="white"
        background-color="#aaa"
        hide-details
        dark
        v-model="entry"
        rows="2" 
        cols="30" 
        resize: auto egg
        outlined
        placeholder="Digite suas notas"
      ></v-textarea>


      <div v-if="entry != ''" class="result">
        <span>{{ makeExit == "" ? "Não encontrado" : makeExit }}</span>
      </div>
    </v-card>
  </div>
</template>

<style scoped>
.result {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;

  color: #fff;

  background: #aaa;

  padding: 10px;
  border-radius: 10px !important;
}
</style>

<script>
export default {
  name: "Home",

  data: () => ({
    entry: "",
    saida: "",

    notes: [
      { note: "c", value: "Dó" },
      { note: "c#", value: "Dó#" },
      { note: "d", value: "Ré" },
      { note: "d#", value: "Ré#" },
      { note: "e", value: "Mi" },
      { note: "f", value: "Fá" },
      { note: "f#", value: "Fá#" },
      { note: "g", value: "Sol" },
      { note: "g#", value: "Sol#" },
      { note: "a", value: "Lá" },
      { note: "a#", value: "Lá#" },
      { note: "b", value: "Si" },
    ],
  }),

  computed: {
    makeExit() {
      let notes = this.entry.replaceAll(",", " ").split(" ");

      let response = "";

      notes.forEach((note) => {
        let nt = note.normalize("NFD").replace(/[\u0300-\u036f]/g, "");
        nt = nt.toLowerCase();

        response =
          this.translate(nt) != null
            ? response + " " + this.translate(nt)
            : response;
      });

      return response;
    },
  },

  methods: {
    translate(note) {
      if (note == "do" || note == "c" || note == "si#" || note == "b#") {
        let index = this.notes.findIndex((x) => x.note == "c");

        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "do#" || note == "c#" || note == "db") {
        let index = this.notes.findIndex((x) => x.note == "c#");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "re" || note == "d") {
        let index = this.notes.findIndex((x) => x.note == "d");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "re#" || note == "d#" || note == "eb") {
        let index = this.notes.findIndex((x) => x.note == "d#");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "mi" || note == "e") {
        let index = this.notes.findIndex((x) => x.note == "e");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "mi#" || note == "e#" || note == "fa" || note == "f") {
        let index = this.notes.findIndex((x) => x.note == "f");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "fa#" || note == "f#" || note == "gb") {
        let index = this.notes.findIndex((x) => x.note == "f#");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "sol" || note == "g") {
        let index = this.notes.findIndex((x) => x.note == "g");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "sol#" || note == "g#" || note == "ab") {
        let index = this.notes.findIndex((x) => x.note == "g#");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "la" || note == "a") {
        let index = this.notes.findIndex((x) => x.note == "a");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "la#" || note == "a#" || note == "bb") {
        let index = this.notes.findIndex((x) => x.note == "a#");
        let position = this.calculate(index);
        return this.notes[position].value;
      } else if (note == "si" || note == "b") {
        let index = this.notes.findIndex((x) => x.note == "b");
        let position = this.calculate(index);
        return this.notes[position].value;
      }
    },

    calculate(index) {
      if (index + 4 > this.notes.length) {
        index -= this.notes.length - 1;
        index += 2;
      } else {
        index += 3;
      }

      return index;
    },
  },
};
</script>
