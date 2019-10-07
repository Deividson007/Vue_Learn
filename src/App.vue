<template>
  <div>
    <div id="slogan" class="text-center">
      <h1>Name</h1>
      <br>
      <h6 class="text-secondary">Gerador de Nomes</h6>
    </div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <h5>Prefixos <span class="badge badge-info">{{ prefixos.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="prefixo in prefixos" v-bind:key="prefixo">
                    <div class="row">
                      <div class="col-md">
                        {{ prefixo }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deletePrefixos(prefix)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br>
                <div class="input-group">
                  <input type="text" class="form-control" v-model="prefix" v-on:keyup.enter="addPrefix(prefix)" placeholder="digite o prefixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addPrefix(prefix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="col-md">
            <h5>Sufixos <span class="badge badge-info">{{ sufixos.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="sufixo in sufixos" v-bind:key="sufixo">
                    <div class="row">
                      <div class="col-md">
                        {{ sufixo }}
                      </div>
                      <div class="col-md text-right">
                        <button class="btn btn-info" v-on:click="deleteSufixos(sufix)">
                          <span class="fa fa-trash"></span>
                        </button>
                      </div>
                    </div>
                  </li>
                </ul>
                <br>
                <div class="input-group">
                  <input type="text" class="form-control" v-model="sufix" v-on:keyup.enter="addSufix(sufix)" placeholder="digite o sufixo">
                  <div class="input-group-append">
                    <button class="btn btn-info" v-on:click="addSufix(sufix)">
                      <span class="fa fa-plus"></span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
        <br>
        <div class="row">
          <div class="col-md">
            <h5>Domains <span class="badge badge-info">{{ domains.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="domain in domains" v-bind:key="domain">
                    {{ domain }}
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
  
<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";

export default {
	name: "app",
	data() {
		return {
			prefix: "",
			sufix: "",
			prefixos: ["Air", "Jet", "Flight"],
			sufixos: ["Hub", "Station", "Mart"],
			domains: ["AirHub", "AirStation", "AirMart", "JetHub", "JetStation", "JetMart", "FlightHub", "FlighStation", "FlightMart"]
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixos.push(prefix);
			this.prefix = "";
			this.generate();
		},
		deletePrefixos(prefix) {
			this.prefixos.splice(this.prefixos.indexOf(prefix), 1);
			this.generate();
		},
		addSufix(sufix) {
			this.sufixos.push(sufix);
			this.sufix = "";
			this.generate();
		},
		deleteSufixos(sufix) {
			this.sufixos.splice(this.sufixos.indexOf(sufix), 1);
			this.generate();
		},
		generate() {
			this.domains = [];
			for(const prefix of this.prefixos) {
				for(const sufix of this.sufixos) {
					this.domains.push(prefix + sufix);
				}
			}
		}
	}
};
</script>

<style>
  #slogan{
    margin-top: 30px;
    margin-bottom: 30px;
  }
  #main{
    background-color: #f1f1f1;
    padding-top: 30px;
    padding-bottom: 30px;
  }
</style>
