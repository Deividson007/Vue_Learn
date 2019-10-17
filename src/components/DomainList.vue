<template>
  <div>
    <div id="main">
      <div class="container">
        <div class="row">
          <div class="col-md">
            <AppItemList title="Prefixos" v-bind:items="prefixos" v-on:addItem="addPrefix" v-on:deleteItem="deletePrefixos"></AppItemList>
          </div>
          <div class="col-md">
            <AppItemList title="Sufixos" v-bind:items="sufixos" v-on:addItem="addSufix" v-on:deleteItem="deleteSufixos"></AppItemList>
          </div>
        </div>
        <br>
        <div class="row">
          <div class="col-md">
            <h5>Domains <span class="badge badge-info">{{ domains.length }}</span></h5>
            <div class="card">
              <div class="card-body">
                <ul class="list-group">
                  <li class="list-group-item" v-for="domain in domains" v-bind:key="domain.name">
                    <div class="row">
                      <div class="col-md">
                        {{ domain.name }}
                      </div>
                      <div class="col-md text-right">
                        <a class="btn btn-info" v-bind:href="domain.checkout" target="_blank">
                          <span class="fa fa-shopping-cart"></span>
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
    </div>
  </div>
</template>
  
<script>
import "bootstrap/dist/css/bootstrap.css";
import "font-awesome/css/font-awesome.css";
import AppItemList from "./AppItemList";

export default {
	name: "app",
	components: {
		AppItemList
	},
	data() {
		return {
			prefixos: ["Air", "Jet", "Flight"],
			sufixos: ["Hub", "Station", "Mart"]
		};
	},
	methods: {
		addPrefix(prefix) {
			this.prefixos.push(prefix);
		},
		deletePrefixos(prefix) {
			this.prefixos.splice(this.prefixos.indexOf(prefix), 1);
		},
		addSufix(sufix) {
			this.sufixos.push(sufix);
		},
		deleteSufixos(sufix) {
			this.sufixos.splice(this.sufixos.indexOf(sufix), 1);
		}
	},
	computed: {
		domains(){
			const domains = [];
			for(const prefix of this.prefixos) {
				for(const sufix of this.sufixos) {
					const name = prefix + sufix;
					const checkout = `https://checkout.hostgator.com.br/?a=add&sld=${name.toLowerCase()}&tld=.com.br`;
					domains.push({
						name,
						checkout
					});
				}
			}
			return domains;
		}
	}
};
</script>

<style>

</style>