<template>
  <div
    class="d-flex justify-center align-center"
    style="background: #18191c; height: 100%"
  >
    <v-card
      class="pa-6"
      color="#c5c5c5"
      max-width="500"
      style="box-shadow: 0px 10px 10px green"
    >
      <v-card-title class="d-flex flex-column justify-center align-center">
        <h2>Jam</h2>
        Transcrever
      </v-card-title>

      <v-textarea
        class="mb-3"
        hide-details
        v-model="entry"
        outlined
        placeholder="Digite suas notas"
      ></v-textarea>

      <p>Resultado:</p>

      <br />

      <span v-if="entry != ''"> Saxofone </span>

      <div v-if="entry != ''" class="result">
        <span>{{ makeExit == "" ? "Não encontrado" : makeExit }}</span>
      </div>
    </v-card>
  </div>
</template>

<style scoped>
.result {
  display: flex;
  justify-content: center;
  align-items: center;

  background: #f5f5f5;

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
        console.log(position);
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
