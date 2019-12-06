<template>
    <div>
        <h5>{{tipo === "sufixo" ? "Sufixos": "Prefixos" }} <span class="badge badge-info">{{items.length}}</span></h5>
          <div class="card">
            <div class="card-body">
              <ul class="list-group">
                <li class="list-group-item" v-for="(item) in items" :key="item">
                  {{item}}
				  <button @click="deletarPrefixoOuSufixo(tipo, item)" class="btn btn-sm btn-danger float-right">
						<i class="fa fa-trash" aria-hidden="true"></i>
					</button>
                </li>
              </ul>
              <br/>
              <div class="input-group">
				<input v-model="inputItem" @keyup.enter="addPrefixoOuSufixo(tipo)" class="form-control" type="text" placeholder="Digite o sufixo"/>
				<div class="input-group-append">
					<button @click="addPrefixoOuSufixo(tipo)" class="btn btn-info"><span class="fa fa-plus"></span></button>
				</div>
			</div>  
        </div>
    </div>
    </div>
</template>

<script>
export default {
    name: 'ListaDeItems',
    props: ["items", "tipo"],
    data() {
        return {
            inputItem: ""
        }
    },
    methods: {
        addPrefixoOuSufixo(tipo) {
			if(tipo === 'prefixo') {
                this.$emit('addPrefixo', this.inputItem);
                this.inputItem = "";	
			}
			if(tipo === 'sufixo') {
                this.$emit('addSufixo', this.inputItem);	
                this.inputItem = "";
			}
		},
		deletarPrefixoOuSufixo(tipo, item) {
			if(tipo === 'prefixo') {
                this.$emit('deletarPrefixo', item);
			}
			if(tipo === 'sufixo') {
				this.$emit('deletarSufixo', item);
			}
		},
    }
}
</script>

<style lang="stylus" scoped>

</style>