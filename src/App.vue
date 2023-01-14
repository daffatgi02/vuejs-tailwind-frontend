<script>
export default{
  data(){
    return{
      listsuhu: []
    }
  },
  methods:{
    async ambildata() {
      const response = await fetch("http://localhost:3000/getlist");
      const data = await response.json();
      this.listsuhu = data.Sensor_suhu
    },
  },
};
</script>

<template>
  <table class="p-10">
    <tr>
      <td>Waktu</td>
      <td>Suhu</td>
    </tr>
    <tr v-for="item in listsuhu">
      <td>{{ item.waktu }}</td>
      <td>{{ item.suhu }}</td>
    </tr>
  </table>

  <div>
    <button class="rounded-3xl p-2 bg-red-500 text-white" @click="ambildata()">Ambil Data</button>
    <button class="rounded-3xl p-2 bg-blue-500 text-white" @click="ambildata()">Testing Button</button>
  </div>
</template>
