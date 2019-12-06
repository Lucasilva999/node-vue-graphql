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
		<ListaDeItems :items="prefixos" tipo="prefixo"
		@addPrefixo="addPrefixo" @deletarPrefixo="deletarPrefixo" />
        </div>
        <div class="col-md">
		<ListaDeItems :items="sufixos" tipo="sufixo"
		@addSufixo="addSufixo" @deletarSufixo ="deletarSufixo"  />
        </div>
      </div>
      <br/>
	  <h5>Domínios <span class="badge badge-info">{{ dominios.length }}</span></h5>
	  		<div class="card">
				<div class="card-body">
					<ul class="list-group">
						<li class="list-group-item" v-for="dominio in dominios" :key="dominio.nome">
							<div class="row">
								<div class="col-md">
									{{ dominio.nome }}
								</div>
								<div class="col-md">
									<a :href="dominio.checkout" target="_blank" role="button" class="btn btn-sm btn-info float-right">
										<i class="fa fa-shopping-cart" aria-hidden="true"></i>
									</a>
								</div>
							</div>
						</li>
					</ul>
				</div>
			</div>
    </div>
  </div>
  </div>
</template>

<script>
//import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import ListaDeItems from './components/ListaDeItems';

export default {
	name: "app",
	components: { ListaDeItems },
	data() {
		return {
			prefixos: ["Air", "Jet", "Flight"],
			sufixos: ["Hub", "Station", "Mart"],
		};
	},
	methods: {
		addPrefixo(e) {
			this.prefixos.push(e);
		},
		addSufixo(e) {
			this.sufixos.push(e);
		},
		deletarPrefixo(e) {
			this.prefixos.splice(this.prefixos.indexOf(e), 1);
		},
		deletarSufixo(e) {
			this.sufixos.splice(this.sufixos.indexOf(e), 1);
		}
	},
	computed: {
			dominios() {
				const dominios = [];
				for ( let prefixo of this.prefixos) {
					for ( let sufixo of this.sufixos) {
						const nome = `${prefixo}${sufixo}`;
						const url = nome.toLowerCase();
						const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${url}&tld=.com.br`;  
						dominios.push({nome, checkout});
					}
				}
				return dominios;
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
