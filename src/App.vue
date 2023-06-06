<template>
  <div class="container grid-lg my-2 text-dark">
    <div class="card">
      <div class="card-header">
        <div class="h4">Exibindo as moedas</div>
      </div>

      <div class="card-body">
        <TabelaMoedas :quotes="quotes" />
      </div>

    </div>

  </div>
</template>

<script>
import TabelaMoedas from './components/TabelaMoedas.vue';
import api from './server/api';
import { onMounted, reactive, toRefs } from 'vue';


export default {
  name: 'App',

  components: {
    TabelaMoedas

  },
//expor API no component
setup() {
  const data = reactive ({ //dados reativos em vuejs

    quotes: {},

  });

  onMounted(async()=> {
    const response = await api.all();
    data.quotes = response.data;
  })

  return {
    ...toRefs(data)
  }

}

}
</script>

<style>
.h4 {
  text-align: center;
  margin-bottom: 10px;
}

.card {
  box-shadow: inset 0 0 1em black, 0 0 1em blueviolet;
}
</style>
