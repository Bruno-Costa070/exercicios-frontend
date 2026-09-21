<template>
    <div class="corpo">
        <h1>Contatos Corporativos</h1>

        <div v-if="carregando">
            <p>Carregando...</p>
        </div>

        <div v-else>
            <div v-for="contato in contatos" :key="contato.id" class="card">
                <h3>{{ contato.name }}</h3>
                <p>E-mail: {{ contato.email }}</p>
                <p>Empresa: {{ contato.company.name }}</p>
            </div>
        </div>

    </div>
</template>

<script>
    export default {
        data() {
            return {
              contatos: [],
              carregando: true
    };
  },
  async mounted() {
    try {
      const resposta = await axios.get('https://jsonplaceholder.typicode.com/users');
      this.contatos = resposta.data;
    } catch (erro) {
      console.error('Erro ao buscar contatos:', erro);
    } finally {
      this.carregando = false;
    }
  }
}
</script>

<style>
    .corpo {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: Arial, sans-serif;
}

.card {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 15px;
  margin-bottom: 15px;
  background-color: #f9f9f9;
}

.card h3 {
  margin-top: 0;
  color: #333;
}
</style>