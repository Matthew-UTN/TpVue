<template>
  <div>
    <b-container fluid style="margin-top: 10px">
    <div class="card" style="margin-left: 10%; width: 60%">
        <div class="row no-gutters">
            <div class="col-auto">
                <b-card-img
                  :src="'/img/' + this.instrumentoEncontrado.imagen"
                  alt="Image"
                  style="min-height:475px; max-height:500px"                  
                ></b-card-img>
            </div>
            <div class="col">
                <div class="card-block px-2" style="margin-top: 20px; text-align: left">
                    <b-card-text style="text-align: left">
                    {{ this.instrumentoEncontrado.cantidadVendida }} vendidos
                    </b-card-text>
                    <b-card-title :title="this.instrumentoEncontrado.instrumento" style="font-size:45px"></b-card-title>
                    <b-card-text style="text-align: left">
                      <h1 style="font-size:80px">$ {{ this.instrumentoEncontrado.precio }}</h1>
                    </b-card-text>
                    <b-card-text style="text-align: left; margin-top:6%">
                      <h5>Marca: {{ this.instrumentoEncontrado.marca }}</h5>
                      <h5>Modelo: {{ this.instrumentoEncontrado.modelo }}</h5>
                    </b-card-text>
                    <b-card-text style="text-align: left; margin-top:6%">
                        <span>Costo envio:</span><br>
                        <b-img src='/img/camion.png' style="color:green" v-if="this.instrumentoEncontrado.costoEnvio == 'G'"></b-img>
                        <span style="color:green" v-if="this.instrumentoEncontrado.costoEnvio == 'G'"> Envió gratis a todo el país</span>
                        <span style="color:orange" v-if="this.instrumentoEncontrado.costoEnvio != 'G'">Costo de Envio Interior de Argentina ${{this.instrumentoEncontrado.costoEnvio}}</span>
                    </b-card-text> 
                </div>
            </div>
        </div>
    </div>
    <div class="container" style="margin-left: 10%; border: 1px solid grey; width: 60%">
        <div class="row no-gutters">
            <div class="col-sm-5" style="text-align:left">
                <span style="text-align: left">Descripcion:</span><br>
                <span> {{this.instrumentoEncontrado.descripcion}}</span>
            </div>
            <div class="col-sm-7" >
                <b-button variant="outline-primary" style="margin-top: 10%; margin-left: -420px">Agregar al carrito</b-button>
            </div>
        </div> 
    </div>
    </b-container>
  </div>
</template>

<script>
export default {
  name: "Detalle",
  components: {},
  mounted() {
    this.getInstrumento();
  },
  data() {
    return {
      instrumentoEncontrado: []
    };
  },
  methods: {
    async getInstrumento() {
      const parametroId = this.$route.params.id;
      const res = await fetch("/instrumentos.json");
      const resJson = await res.json();
      console.log(resJson);
      this.instrumentoEncontrado = await resJson.instrumentos.find(
        instrumento => instrumento.id === parametroId
      );
      console.log(this.instrumentoEncontrado);
    }
  }
};
</script>