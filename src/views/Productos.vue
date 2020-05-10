<template>
  <div class="productos">
    <b-container fluid >
      <b-card-group deck style="margin-left: 20px">
        <div
          v-for="instrumento in instrumentosData"
          :key="instrumento.id"
          style="margin-top:15px"
        >
          <instrumento-item :instrumentoParam="instrumento"></instrumento-item>
        </div>
      </b-card-group>
    </b-container>
  </div>
</template> 

<script>
// @ is an alias to /src
import Instrumento from "@/components/Instrumento.vue";

export default {
  name: "Productos",
  components: {
    "instrumento-item": Instrumento
  },
  mounted() {
    this.getInstrumentos();
  },
  data() {
    return {
      instrumentosData: []
    };
  },
  methods: {
    async getInstrumentos() {
      const res = await fetch("/instrumentos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.instrumentosData = resJson.instrumentos;
    }
  }
};
</script>
