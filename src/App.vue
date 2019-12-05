<template>
  <div>
    <div id="app">
    <div class="text-center">
      <h1>Name Gator</h1>
      <br/>
      <h6 class="text-secondary">Gerador de Nomes Utilizando Vue, GraphQL e Node</h6>
    </div>
  </div>
  <div id="main">
    <div class="container">
      <div class="row">
        <div class="col-md">
          <h5>Prefixos <span class="badge badge-info">0</span></h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="prefixo in prefixos" :key="prefixo">
                  {{prefixo}}
					<button @click="deletarPrefixoOuSufixo('prefixo', prefixo)" class="btn btn-sm btn-danger float-right">
						<i class="fa fa-trash" aria-hidden="true"></i>
					</button>
                </li>
              </ul>
			<br/>
			<div class="input-group">
				<input v-model="inputPrefixo" @keyup.enter="addPrefixoOuSufixo('prefixo')" class="form-control" type="text" placeholder="Digite o prefixo"/>
				<div class="input-group-append">
					<button @click="addPrefixoOuSufixo('prefixo')" class="btn btn-info"><span class="fa fa-plus"></span></button>
				</div>
			</div>  
            </div>
          </div>
        </div>
        <div class="col-md">
          <h5>Sufixos <span class="badge badge-info">0</span></h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="sufixo in sufixos" :key="sufixo">
                  {{sufixo}}
				  <button @click="deletarPrefixoOuSufixo('sufixo', sufixo)" class="btn btn-sm btn-danger float-right">
						<i class="fa fa-trash" aria-hidden="true"></i>
					</button>
                </li>
              </ul>
              <br/>
              <div class="input-group">
				<input v-model="inputSufixo" @keyup.enter="addPrefixoOuSufixo('sufixo')" class="form-control" type="text" placeholder="Digite o sufixo"/>
				<div class="input-group-append">
					<button @click="addPrefixoOuSufixo('sufixo')" class="btn btn-info"><span class="fa fa-plus"></span></button>
				</div>
			</div>  
            </div>
          </div>
        </div>
      </div>
      <br/>
			<h5>Domínios <span class="badge badge-info">{{ dominios.length }}</span></h5>
				<div class="card">
					<div class="card-body">
						<ul class="list-group">
							<li class="list-group-item" v-for="dominio in dominios" :key="dominio">
								{{ dominio }}
							</li>
						</ul>
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
			inputPrefixo: '',
			inputSufixo: '',
			prefixos: ["Air", "Jet", "Flight"],
			sufixos: ["Hub", "Station", "Mart"],
			dominios: ['teste']
		};
	},
	methods: {
		addPrefixoOuSufixo(tipo) {
			if(tipo === 'prefixo') {
				this.prefixos.push(this.inputPrefixo);
				this.inputPrefixo = "";
				this.gerarDominios();
			}
			if(tipo === 'sufixo') {
				this.sufixos.push(this.inputSufixo);
				this.inputSufixo = "";
				this.gerarDominios();
			}
		},
		deletarPrefixoOuSufixo(tipo, index) {
			if(tipo === 'prefixo') {
				this.prefixos.splice(this.prefixos.indexOf(index), 1);
				this.gerarDominios();
			}
			if(tipo === 'sufixo') {
				this.sufixos.splice(this.sufixos.indexOf(index), 1);
				this.gerarDominios();
			}
		},
		gerarDominios() {
			this.dominios = [];
			for ( let prefixo of this.prefixos) {
				for ( let sufixo of this.sufixos) {
					this.dominios.push(`${prefixo}${sufixo}`);
				}
			}
		}, 
		mounted() {
			this.gerarDominios();
		}
	},
	
};
</script>

<style>
#app {
  margin-top: 30px;
  margin-bottom: 30px;
}

#main {
  background-color: #f1f1f1;
  padding-top: 30px;
  padding-bottom: 30px;
}
</style>
