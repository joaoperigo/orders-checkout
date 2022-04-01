<template>
<div class="form-group client-name-group mt-4 pt-2 sticky-top" id="wrapper-barra-busca">
    <!-- <label for="barra-busca" class="w-100"><h2>Pesquisar</h2></label> -->
    <div class="input-group d-flex justify-content-end">
        <input type="text" class="form-control barra-busca" placeholder="Digite o id ou nome do produto" aria-label="Recipient's username" aria-describedby="button-addon2" id="barra-busca" ref="focaBar" v-model="inputValorBusca">
        <button class="btn btn-outline-secondary botao-busca" type="button" id="bt-busca" v-show="checaBt" @click="buscaProduto($event)">
          <img src="@/assets/lupa.svg" alt="" class="img-fluid">
        </button>
        <button class="btn btn-outline-secondary botao-busca" type="button" id="bt-busca-sobe" v-show="!checaBt" @click="toTop(); buscaProduto($event)">
          <img src="@/assets/lupa.svg" alt="" class="img-fluid">
        </button>
    </div>
</div>
<p class="small m-0 text-start">*Para buscar por ID digite um numero, por nome digite o nome.</p>
</template>

<script>
export default {
    name: 'SearchBar',
    data() {
    return {
      windowTop: 0,
      checaBt: true,
      inputValorBusca: null
    };
  },
  mounted() {
    window.addEventListener("scroll", this.onScroll);
  },
  beforeDestroy() {
    window.removeEventListener("scroll", this.onScroll);
  },
  methods: {
    onScroll(e) {
        this.windowTop = e.target.documentElement.scrollTop;
        //   console.log(this.$refs.foo.offsetTop); // it will focus the input having ref="foo"
        const wrapperBusca = document.getElementById("wrapper-barra-busca")
        const barraBusca = document.getElementById("barra-busca")
        //const topPos = wrapperBusca.offsetTop
        const iniPos = wrapperBusca.getBoundingClientRect().top
        console.log(iniPos)
        if (iniPos < 70) {
            // console.log("sim")
            barraBusca.style.display="none"
            this.checaBt = false
        }
        else {
            // console.log("nao")
            barraBusca.style.display="block"
            this.checaBt = true
        }
    },
    toTop () {
        window.scrollTo({
          top: 0,
          behavior: "smooth"
        });
        // inserir focus na barra ao clicar
        setTimeout(() => {
            this.$refs.focaBar.focus()
        }, 800)
    },
    buscaProduto(e) {
      if(this.inputValorBusca!=null) 
        this.$emit('clicouBusca', this.inputValorBusca)
    }
  },
  emits: ['clicouBusca']
}
</script>
<style scoped>
  #wrapper-barra-busca {
      pointer-events: none;
  }
  #wrapper-barra-busca * {
      pointer-events: auto;
  }
</style>