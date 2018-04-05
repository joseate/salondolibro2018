<template>
  <div id="app">
  <section class="jumbotron text-center">
      <div class="container">
        <h1 class="jumbotron-heading">Sal&oacute;n do Libro 2018</h1>
        <p class="lead text-muted">Calendario <i>non oficial</i> das actividades do Sal&oacute;n do Libro de Pontevedra 2018.<br>
        Realizado coa informaci&oacute;n contida no  <a href="http://www.salondolibro.gal/programacion-2018/" target="blank">programa oficial</a> do Sal&oacute;n do Libro na s&uacute;a primeira edici&oacute;n</p>
        <p>
          <button @click="mostrarFiltros = !mostrarFiltros" class="btn btn-primary" type="button" data-toggle="collapse" data-target="#collapseExample" aria-expanded="false" aria-controls="collapseExample">
            {{textButtonFiltros}}
          </button>
        </p>
        <div id="accordion" v-if="mostrarFiltros">

          <div class="card" v-if="dias">
            <div class="card-header"  id="headingOne">
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseOne" aria-expanded="true" aria-controls="collapseOne" style="width: 188px;">Xornadas</button>
              </div>
              <div class="float-right" v-if="checkedDias.length == 1">{{checkedDias.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedDias.length > 1">{{checkedDias.length}} filtros seleccionados</div>
            </div>
            <div id="collapseOne" class="collapse" aria-labelledby="headingOne" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="dia in dias" v-bind:key="dia">
                  <span v-if="dia">
                    <input class="form-check-input" type="checkbox" :id="dia" v-model="checkedDias" :value="dia">
                    <label class="form-check-label" :for="dia" style="width: 86px;">{{dia}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>

          <div class="card" v-if="horas">
            <div class="card-header"  id="headingTwo">
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseTwo" aria-expanded="true" aria-controls="collapseTwo" style="width: 188px;">Horas actividades</button>
              </div>
              <div class="float-right" v-if="checkedHoras.length == 1">{{checkedHoras.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedHoras.length > 1">{{checkedHoras.length}} filtros seleccionados</div>
            </div>
            <div id="collapseTwo" class="collapse" aria-labelledby="headingTwo" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="hora in horas" v-bind:key="hora">
                  <span v-if="hora">
                    <input class="form-check-input" type="checkbox" :id="hora" v-model="checkedHoras" :value="hora">
                    <label class="form-check-label" :for="hora">{{hora}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>


          <div class="card" v-if="categorias">
            <div class="card-header"  id="headingThree">
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseThree" aria-expanded="true" aria-controls="collapseThree" style="width: 188px;">Categor&iacute;as</button>
              </div>
              <div class="float-right" v-if="checkedCategorias.length == 1">{{checkedCategorias.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedCategorias.length > 1">{{checkedCategorias.length}} filtros seleccionados</div>
            </div>
            <div id="collapseThree" class="collapse" aria-labelledby="headingThree" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="categoria in categorias" v-bind:key="categoria">
                  <span v-if="categoria">
                    <input class="form-check-input" type="checkbox" :id="categoria" v-model="checkedCategorias" :value="categoria">
                    <label class="form-check-label" :for="categoria">{{categoria}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>


          <div class="card" v-if="lugares">
            <div class="card-header"  id="headingFour"> 
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseFour" aria-expanded="true" aria-controls="collapseFour" style="width: 188px;">Lugares</button>
              </div>
              <div class="float-right" v-if="checkedLugares.length == 1">{{checkedLugares.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedLugares.length > 1">{{checkedLugares.length}} filtros seleccionados</div>                
            </div>
            <div id="collapseFour" class="collapse" aria-labelledby="headingFour" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="lugar in lugares" v-bind:key="lugar">
                  <span v-if="lugar">
                    <input class="form-check-input" type="checkbox" :id="lugar" v-model="checkedLugares" :value="lugar">
                    <label class="form-check-label text-truncate" :for="lugar">{{lugar}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>


          <div class="card" v-if="idades">
            <div class="card-header"  id="headingFive">
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseFive" aria-expanded="true" aria-controls="collapseFive" style="width: 188px;">Idades recomendadas</button>
              </div>
              <div class="float-right" v-if="checkedIdades.length == 1">{{checkedIdades.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedIdades.length > 1">{{checkedIdades.length}} filtros seleccionados</div>  
            </div>
            <div id="collapseFive" class="collapse" aria-labelledby="headingFive" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="idade in idades" v-bind:key="idade">
                  <span v-if="idade">
                    <input class="form-check-input" type="checkbox" :id="idade" v-model="checkedIdades" :value="idade">
                    <label class="form-check-label" :for="idade">{{idade}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>
      

          <div class="card" v-if="inscricions">
            <div class="card-header"  id="headingSix">
              <div class="float-none">
                <button class="btn btn-info collapsed" data-toggle="collapse" data-target="#collapseSix" aria-expanded="true" aria-controls="collapseSix" style="width: 188px;">Tipos inscrici&oacute;ns</button>
              </div>
              <div class="float-right" v-if="checkedInscricions.length == 1">{{checkedInscricions.length}} filtro seleccionado</div>
              <div class="float-right" v-if="checkedInscricions.length > 1">{{checkedInscricions.length}} filtros seleccionados</div>                  
            </div>
            <div id="collapseSix" class="collapse" aria-labelledby="headingSix" data-parent="#accordion">
              <div class="card-body">            
                <div class="form-check form-check-inline" v-for="inscricion in inscricions" v-bind:key="inscricion">
                  <span v-if="inscricion">
                    <input class="form-check-input" type="checkbox" :id="inscricion" v-model="checkedInscricions" :value="inscricion">
                    <label class="form-check-label" :for="inscricion">{{inscricion}}</label>
                  </span>
                </div>  
              </div>   
            </div>
          </div>      
        </div>          
      </div>
      <h1 class="display-4" v-if="filteredActividades.length == 0">Non hai actividades cos criterios de b&uacute;squeda</h1>
      <h1 class="display-4" v-if="filteredActividades.length == 1">Atopaches {{filteredActividades.length}} actividade</h1>
      <h1 class="display-4" v-if="filteredActividades.length > 1">Atopaches {{filteredActividades.length}} actividades</h1>
      <h3 class="display-5" v-if="favoritos.length == 1">Xa t&eacute;s marcado {{favoritos.length}} favorito</h3>
      <h3 class="display-5" v-if="favoritos.length > 1">Xa t&eacute;s marcados {{favoritos.length}} favoritos</h3>
      <div v-if="favoritos.length >= 1">
        <input class="form-check-input" type="checkbox" id="filtroFavoritos" v-model="filtroFavoritos" :value="filtroFavoritos">
        <label class="form-check-label" for="filtroFavoritos">Ver s&oacute; os meus favoritos</label>
      </div>
    </section>
    <div class="container">
      <div class="row">
        <div class="col-12 col-sm-12 col-md-6 col-ld-4" v-for="actividad in filteredActividades" v-bind:key="actividad._id">
          <div class="card box-shadow">               
          <div class="card-header">
            <div class="d-flex justify-content-around">
              <span><small>{{actividad.dia}}</small></span> 
              <span>{{actividad.hora_inicio}}</span>
              <span v-if="actividadeFamiliar(actividad.publico_familiar)">
                <img src="./assets/1495911998-300px.png" alt="Público familiar" width="30rem" height="30rem" data-toggle="tooltip" data-placement="top" title="Público familiar">
              </span>
              <span v-if="inscricionPrevia(actividad.inscricion_previa)">
                <img src="./assets/edit-icon-300px.png" alt="Inscricion previa" width="25rem" height="25rem" data-toggle="tooltip" data-placement="top" title="Inscrión previa">
              </span> 
              <div>
                <button @click="marcarFavorito(actividad._id)" class="btn" :class="esFavorito(actividad._id) ? 'btn-warning' : 'btn-secondary'">G&uacute;stame</button>
              </div>
            </div>
          </div>
            <div class="card-body">
              <h6 class="text-info">{{actividad.categoria}}</h6>
              <h3 class="card-title">{{actividad.titulo}}</h3>
              <h4 class="card-subtitle mb-2 text-muted">{{actividad.subtitulo}}</h4>                  
              <p class="card-text" >{{actividad.texto}}</p>
                <ul class="list-group list-group-flush">
                  <li class="list-group-item" v-if="actividad.ubicacion"><small>{{actividad.ubicacion}}</small></li>
                  <li class="list-group-item" v-if="actividad.idade_recomendada" :class="{'text-danger': actividad.idade_recomendada == 'Público adulto'}"><small>{{actividad.idade_recomendada}}</small></li>
                  <li class="list-group-item" :class="{'text-danger': inscricionPrevia(actividad.inscricion_previa)}" v-if="actividad.inscricion"><small>{{actividad.inscricion}} <span v-if="actividad.capacidade"> | {{actividad.capacidade}}</span></small></li>
                  <li class="list-group-item" v-if="actividad.prezo"> <small class="text-muted">{{actividad.prezo}}</small></li>
                </ul>
            </div>
          </div>
        </div>
      </div>
    </div>      
  </div>

</template>

<script>
import axios from "axios";
import actividadesJson from "./actividades.json";

export default {
  name: "app",
  data() {
    return {
      actividades: [],
      mostrarFiltros: false,
      dias: [],
      checkedDias: [],
      horas: [],
      checkedHoras: [],
      categorias: [],
      checkedCategorias: [],
      lugares: [],
      checkedLugares: [],
      idades: [],
      checkedIdades: [],
      inscricions: [],
      checkedInscricions: [],
      favoritos: [],
      filtroFavoritos: false
    };
  },
  created: function() {
    this.getFavoritos();
    this.getActividades();
  },
  computed: {
    filteredActividades() {
      let filtros = {};
      if (this.checkedDias.length) {
        filtros["dia"] = this.checkedDias;
      }
      if (this.checkedHoras.length) {
        filtros["hora_inicio"] = this.checkedHoras;
      }
      if (this.checkedCategorias.length) {
        filtros["categoria"] = this.checkedCategorias;
      }
      if (this.checkedLugares.length) {
        filtros["ubicacion"] = this.checkedLugares;
      }
      if (this.checkedIdades.length) {
        filtros["idade_recomendada"] = this.checkedIdades;
      }
      if (this.checkedInscricions.length) {
        filtros["inscricion"] = this.checkedInscricions;
      }
      if (this.filtroFavoritos) {
        filtros["_id"] = this.favoritos;
      }

      // return this.actividades.filter(j => this.checkedDias.includes(j.dia));
      const filterKeys = Object.keys(filtros);
      // filters all elements passing the criteria
      return this.actividades
        .filter(eachObj => {
          return filterKeys.every(eachKey => {
            if (!filtros[eachKey].length) {
              return true; // passing an empty filter means that filter is ignored.
            }
            return filtros[eachKey].includes(eachObj[eachKey]);
          });
        })
        .sort(function(a, b) {
          var fecha1 = a.dia.split(/\D/);
          var fecha2 = b.dia.split(/\D/);
          var hora1 = a.hora_inicio.split(':');
          var hora2 = b.hora_inicio.split(':');
          return (
            new Date(fecha1[2], fecha1[1], fecha1[0], hora1[0], hora1[1]) -
            new Date(fecha2[2], fecha2[1], fecha2[0], hora2[0], hora2[1])
          );
        });
    },
    textButtonFiltros() {
      if (this.mostrarFiltros) {
        return "Ocultar Filtros";
      } else {
        return "Mostrar Filtros";
      }
    }
  },
  methods: {
    getFavoritos: function () {
      this.favoritos = JSON.parse(localStorage.getItem("SDL.actividades.fav")) || [] ;
    },
    getActividades: function() {
      this.actividades = [];
      this.dias = [...new Set(actividadesJson.map(item => item.dia))].sort();
      this.horas = [
        ...new Set(actividadesJson.map(item => item.hora_inicio))
      ].sort();
      this.categorias = [
        ...new Set(actividadesJson.map(item => item.categoria))
      ].sort();
      this.lugares = [
        ...new Set(actividadesJson.map(item => item.ubicacion))
      ].sort();
      this.idades = [
        ...new Set(
          actividadesJson
            .map(item => item.idade_recomendada)
            .filter((value, index, self) => self.indexOf(value) === index)
        )
      ].sort();
      this.inscricions = [
        ...new Set(actividadesJson.map(item => item.inscricion))
      ].sort();
      this.actividades = actividadesJson;
    },
    inscricionPrevia: function (value) {
      return value == 'true';
    },
    actividadeFamiliar: function (value) {
      return value == 'true';
    },
    marcarFavorito: function (value) {
      if (!this.favoritos.includes(value)) {
        this.favoritos.push(value)
      } else {
        var borrado = this.favoritos.splice(this.favoritos.indexOf(value),1);
      }
      this.actualizarLocalStorage();
    },
    desmarcarFavorito: function (value) {
      var borrado = this.favoritos.splice(this.favoritos.indexOf(value));
      this.actualizarLocalStorage();
    },
    esFavorito: function (value) {
      return this.favoritos.includes(value);
    },
    actualizarLocalStorage: function () {
      localStorage.setItem("SDL.actividades.fav", JSON.stringify(this.favoritos));
    }
  }
};
</script>

<style lang="scss">

</style>
